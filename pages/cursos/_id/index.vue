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
          <!-- caso alumnos -->
          <CoursesCurso
            :curso="curso"
            :evaluaciones="evaluaciones"
            :promedioE="promedioE"
          />
        </div>
        <div v-if="curso.can_edit === true">
          <SubjectAdminCurso
            :curso="curso"
            :todasEvaluaciones="todasEvaluaciones"
            :evaluacionesG="evaluacionesG"
            :promedioE="promedioE"
            :alumnos="alumnos"
            :coordinaciones="coordinaciones"
          />
        </div>
        <!--
        <div v-else>Ha ocurrido un error al mostrar el curso</div>
        -->
      </v-container>
    </v-container>
  </div>
</template>

<script>
export default {
  props: ["curso", "alumnos"],
  layout: "logged",
  data() {
    return {
      evaluaciones: [],
      todasEvaluaciones: [],
      evaluacionesG: [],
      coordinaciones: [],
      promedioE: 0,
    };
  },
  created() {
    //Caso alumnos
    if (!this.curso.can_edit) {
      this.getEvaluations();
    }
    if (this.curso.can_edit) {
      //Caso profe
      this.getEvaluationsGeneral();
      this.getAll();
      this.getCoordinaciones();
    }
  },
  methods: {
    volver() {
      this.$router.go(-1);
      this.$nuxt.refresh();
    },
    //DATA : evaluaciones
    // Caso alumno :
    getEvaluations() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/user/" +
            this.$route.params.id +
            "/"
        )
        .then((res) => {
          var evaluaciones = res.data.evaluations;
          this.evaluaciones = evaluaciones;
          this.promedioE = evaluaciones[0].promedio;
          console.log(evaluaciones);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
    //Caso profesor
    //DATA : todasEvaluaciones
    getAll() {
      this.$axios
        .get(
          process.env.baseUrl +
            "evaluations/promedio/course/" +
            this.$route.params.id +
            "/"
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
    // DATA : evaluacionesG
    getEvaluationsGeneral() {
      this.$axios
        .get(
          process.env.baseUrl +
            "evaluations/course/" +
            this.$route.params.id +
            "/"
        )
        .then((res) => {
          var evaluaciones = res.data.evaluations;
          this.evaluacionesG = evaluaciones;
          console.log("EVALUACIONES : ", evaluaciones);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getCoordinaciones() {
      this.$axios
        .get(
          process.env.baseUrl +
            "courses/coursecordination/" +
            this.$route.params.id +
            "/"
        )
        .then((res) => {
          this.coordinaciones = res.data.coordinaciones;
          console.log("COORDINACIONES ::::" + this.coordinaciones);
        })
        .catch((error) => {
          console.log(error);
          this.coordinaciones = [];
        });
    },
  },
};
</script>
