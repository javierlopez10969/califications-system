<template>
  <v-container fill-height fluid>
    <v-row>
      <v-btn outlined depressed small @click="volver">
        <v-icon dark left> mdi-arrow-left</v-icon>
        Volver a cursos
      </v-btn>
    </v-row>
    <div v-if="curso">
      <div v-if="todasEvaluaciones.length === 0">
        <CoursesCurso
          :cursos="cursos"
          :curso="curso"
          :evaluaciones="evaluaciones"
          :todasEvaluaciones="todasEvaluaciones"
          :promedioE="promedioE"
          :alumnos="alumnos"
        />
      </div>
      <div v-else>
        <SubjectAdminCurso
          :curso="curso"
          :todasEvaluaciones="todasEvaluaciones"
          :promedioE="promedioE"
          :alumnos="alumnos"
        />
      </div>
    </div>
  </v-container>
</template>
<script>
import Courses from "../../../components/Courses/Cursos.vue";
export default {
  components: { Courses },
  ssr: false,
  layout: "logged",
  props: ["semestre"],
  data() {
    return {
      curso: {},
      cursos: [],
      evaluaciones: [],
      todasEvaluaciones: [],
      evaluacionesG: [],
      alumnos: [],
      promedioE: 0,
    };
  },
  created() {
    this.getCourses();
    this.findCurso();
    this.getEvaluations();
    this.getAllEvaluations();
    this.getAlumns();
  },

  methods: {
    volver() {
      this.$router.go(-1);
      this.$nuxt.refresh();
    },
    async findCurso() {
      let id = +this.$route.params.id;
      this.curso = this.cursos.find((curso) => curso.id === id);
    },
    async getCourses() {
      try {
        const res = await this.$axios.post(
          process.env.baseUrl + "courses/list/",
          { token: this.$auth.strategy.token.get().slice(7) }
        );
        var cursos = res.data.courses;
        this.cursos = cursos;
        this.findCurso();
      } catch (error) {
        console.log(error);
        this.registro = [];
      }
    },
    async getAllEvaluations() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/promedio/course/" +
            this.$route.params.id +
            "/",
          {
            token: this.$auth.strategy.token.get().slice(7),
          }
        )
        .then((res) => {
          var todasEvaluaciones = res.data;
          this.todasEvaluaciones = todasEvaluaciones;
          console.log(todasEvaluaciones);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
    async getEvaluations() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/user/" +
            this.$route.params.id +
            "/",
          {
            token: localStorage.getItem("token"),
          }
        )
        .then((res) => {
          var evaluaciones = res.data.evaluations;
          this.evaluaciones = evaluaciones;
          console.log(evaluaciones);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
    async getAlumns() {
      this.$axios
        .get(
          process.env.baseUrl + "courses/users/" + this.$route.params.id + "/"
        )
        .then((res) => {
          var alumns = res.data.alumns;
          this.alumnos = alumns;
          console.log(alumns[0].email);
          console.log("ALUMNOS :" + this.alumnos);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
    async getEvaluationsGeneral() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/course/" +
            this.$route.params.id +
            "/",
          {
            token: this.$auth.strategy.token.get().slice(7),
          }
        )
        .then((res) => {
          var evaluaciones = res.data.evaluations;
          this.evaluacionesG = evaluaciones;
          console.log(evaluaciones);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
  },
  computed: {
    course() {
      return this.cursos.find((curso) => curso.id === this.$route.params.id);
    },
  },
};
</script>