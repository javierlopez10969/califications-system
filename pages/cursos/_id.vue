<template>
  <div>
    Tus cursos son :
    <v-spacer></v-spacer>
    <CoursesCursos :cursos="cursos" />
    <v-spacer></v-spacer>
    <CoursesCurso :curso="curso" />
  </div>
</template>
<script>
export default {
  name: "cursos",
  layout: "logged",
  props: ["cursos"],
  data() {
    return {
      curso: {},
      id: "",
    };
  },
  updated() {
    this.findCurso();
  },
  methods: {
    findCurso() {
      let id = +this.$route.params.id;
      console.log(id);
      this.curso = this.cursos.find((curso) => curso.id === id);
    },
  },
};
</script>