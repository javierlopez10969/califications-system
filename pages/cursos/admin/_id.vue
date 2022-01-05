<template>
  <div>
    <RegistroCurso :cursos="cursos" :curso="curso" />
    <NuxtLink to="/cursos">Volver a mis cursos</NuxtLink>
    <SubjectAdminAlumnList :alumnos.sync="alumnos" />

    <RegistroCalifications :evaluaciones="evaluacionesG" :fecha="fecha" />
  </div>
</template>
<script>
export default {
  layout: "logged",
  props: ["cursos"],
  data() {
    return {
      curso: {},
      id: "",
      alumnos: [],
      evaluacionesG: [],
    };
  },
  async beforeMount() {
    this.findCurso();
    this.getAlumns();
    this.getEvaluationsGeneral();
  },

  methods: {
    async findCurso() {
      let id = +this.$route.params.id;
      console.log(id);
      this.curso = this.cursos.find((curso) => curso.id === id);
    },
    async getAlumns() {
      this.$axios
        .get(
          process.env.baseUrl + "courses/users/" + this.$route.params.id + "/"
        )
        .then((res) => {
          var alumns = res.data.alumns;
          this.alumnos = alumns;
          console.log(alumns[0].email);
          console.log("ALUMNOS :" + this.alumnos);
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
