<template>
  <div>
    <CoursesCurso :cursos="cursos" :curso="curso" />
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
  created() {
    this.findCurso();
  },

  methods: {
    async findCurso() {
      let id = +this.$route.params.id;
      console.log(id);
      this.curso = this.cursos.find((curso) => curso.id === id);
    },
  },
};
</script>