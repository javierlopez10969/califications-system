<template>
  <v-container fluid>
    <ButtonVolver :text="`Volver a registro`" />
    <RegistroCurso :curso="curso" :evaluaciones="evaluaciones" />
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
    };
  },
  async asyncData({ $axios, params }) {
    let res = await $axios.get("/courses/" + params.id + "/");
    let curso = res.data;
    return { curso };
  },
  async created() {
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
            token: this.$auth.strategy.token.get().slice(7),
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