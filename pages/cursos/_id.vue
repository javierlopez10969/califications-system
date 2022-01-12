<template>
  <div>
    {{todasEvaluaciones}}
    <nuxt-child
      :curso="curso"
      :alumnos="alumnos"
      :todasEvaluaciones="todasEvaluaciones"
      :evaluaciones="evaluaciones"
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
    console;
    let curso = res.data.course;
    //Caso alumno

    //Caso administrador del curso

    // Usuarios inscritos en el curso
    res = await $axios.get("courses/alumns/" + params.id + "/");
    var alumnos = res.data.alumns;
    res = $axios.get("evaluations/promedio/course/"+params.id +"/")
    var todasEvaluaciones = res.data;
    console.log("EVALUACIONES : "+todasEvaluaciones)

    return {
      curso,
      alumnos,
      todasEvaluaciones
    };
  },
};
</script>
<style lang="scss" scoped>
</style>