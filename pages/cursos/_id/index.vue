<template>
  <div>
    <v-container fluid>
      <ButtonVolver :text="`Volver a cursos`" />
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
            :evaluaciones="evaluaciones"
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
  props: ["curso", "alumnos", "coordinaciones", "todasEvaluaciones"],
  layout: "logged",
  data() {
    return {
      evaluaciones: [],
      evaluacionesG: [],
      promedioE: 0,
    };
  },
  created() {
    //Caso alumnos
    if (!this.curso.can_edit) {
      this.getEvaluations();
    }
    if (this.curso.can_edit) {
      this.getEvaluationsGeneral();
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
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
