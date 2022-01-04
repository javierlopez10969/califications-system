<template>
  <v-container>
    <RegistroCurso :curso="curso" />
    <RegistroCalifications :evaluaciones="evaluaciones" />
    <RegistroCalifications :evaluaciones="evaluacionesG" :fecha="fecha" />
  </v-container>
</template>

<script>
export default {
  props: ["registro"],
  layout: "logged",
  data() {
    return {
      curso: {},
      evaluaciones: [],
      evaluacionesG : [],
      fecha: true,
    };
  },
  beforeMount() {
    this.findCurso();
    this.getEvaluations();
    this.getEvaluationsGeneral();
  },
  methods: {
    async findCurso() {
      let id = +this.$route.params.id;
      console.log(id);
      this.curso = this.registro.find((curso) => curso.id === id);
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
    async getEvaluationsGeneral() {
      this.$axios
        .post(
          process.env.baseUrl +
            "evaluations/course/" +
            this.$route.params.id +
            "/",
          {
            token: localStorage.getItem("token"),
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