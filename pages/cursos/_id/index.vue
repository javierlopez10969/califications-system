<template>
  <div>
    <v-container fluid>
      <v-row>
        <v-btn outlined depressed small @click="volver">
          <v-icon dark left> mdi-arrow-left</v-icon>
          Volver a cursos
        </v-btn>
      </v-row>
      <v-container fluid v-if="curso">
        <div v-if="curso.can_edit === false">
          <CoursesCurso
            :cursos="cursos"
            :curso="curso"
            :evaluaciones="evaluaciones"
            :todasEvaluaciones="todasEvaluaciones"
            :promedioE="promedioE"
            :alumnos="alumnos"
          />
        </div>
        <div v-if="curso.can_edit === true">
          <SubjectAdminCurso
            :curso="curso"
            :todasEvaluaciones="todasEvaluaciones"
            :promedioE="promedioE"
            :alumnos="alumnos"
          />
        </div>
        <div v-else>Ha ocurrido un error al mostrar el curso</div>
      </v-container>
    </v-container>
  </div>
</template>

<script>
export default {
  props: ["curso"],
  head: {
    title: "Curso",
  },
  data() {
    return {
      evaluaciones: [],
      todasEvaluaciones: [],
      evaluacionesG: [],
      alumnos: [],
      promedioE: 0,
    };
  },
  created() {
    this.getEvaluations();
    this.getAllEvaluations();
    this.getAlumns();
  },
  methods: {
    volver() {
      this.$router.go(-1);
      this.$nuxt.refresh();
    },

    getAllEvaluations() {
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
    getEvaluations() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/user/" +
            this.$route.params.id +
            "/",
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
    getAlumns() {
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
    getEvaluationsGeneral() {
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
};
</script>
