<template>
  <v-container fill-height fluid>
    {{curso}}
    <CoursesCurso
      :cursos="cursos"
      :curso.sync="curso"
      :evaluaciones="evaluaciones"
      :todasEvaluaciones="todasEvaluaciones"
      :promedioE="promedioE"
      :alumnos="alumnos"
    />
  </v-container>
</template>
<script>
import Courses from "../../components/Courses/Cursos.vue";
export default {
  components: { Courses },
  layout: "logged",
  props: ["semestre"],
  data() {
    return {
      curso: {},
      cursos: {},
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
    async findCurso() {
      let id = +this.$route.params.id;
      console.log("ID FUNCTION" + id);
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
          this.promedioE = this.evaluaciones[0].promedio;
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
  updated() {
    this.findCurso();
  },
};
</script>