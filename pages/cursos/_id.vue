<template>
  <div>
    <CoursesCurso
      :cursos="cursos"
      :curso="curso"
      :evaluaciones="evaluaciones"
      :todasEvaluaciones="todasEvaluaciones"
    />

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
      evaluaciones: [],
      todasEvaluaciones: [],
      fecha: true,
    };
  },
  created() {
    this.findCurso();
    this.getEvaluations();
    this.getAllEvaluations();
  },

  methods: {
    async findCurso() {
      let id = +this.$route.params.id;
      console.log(id);
      this.curso = this.cursos.find((curso) => curso.id === id);
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
    async getAllEvaluations() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/promedio/course/" +
            this.$route.params.id +
            "/",
          {
            token: localStorage.getItem("token"),
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
  },
};
</script>