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
</template>

<script>
export default {
  props: ["curso"],
  methods: {
    volver() {
      this.$router.go(-1);
    },
  },
};
</script>