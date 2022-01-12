<template>
  <div>
    <nuxt-child
      :curso="curso"
      :alumnos="alumnos"
      :todasEvaluaciones="todasEvaluaciones"
      :coordinaciones="coordinaciones"
    />
  </div>
</template>

<script>
export default {
  layout: "logged",
  head() {
    return {
      title: "",
      titleTemplate: `%s ${this.curso.name}`,
    };
  },
  async asyncData({ $axios, params }) {
    let res = await $axios.post("/courses/" + params.id + "/");
    let curso = res.data.course;
    //Caso alumno

    //Caso administrador del curso

    // Usuarios inscritos en el curso
    if (curso.can_edit) {
      res = await $axios.get("courses/alumns/" + params.id + "/");
      var alumnos = res.data.alumns;
      res = await $axios.get("evaluations/promedio/course/" + params.id + "/");
      var todasEvaluaciones = res.data;
      res = await $axios.get("courses/coursecordination/" + params.id + "/");
      var coordinaciones = res.data.coordinaciones;
    }else{
      alumnos = null;
      todasEvaluaciones = null;
      coordinaciones = null;
    }
    return {
      curso,
      alumnos,
      todasEvaluaciones,
      coordinaciones,
    };
  },
};
</script>
<style lang="scss" scoped>
</style>