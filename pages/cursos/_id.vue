<template>
  <div>
    <CoursesCurso
      :cursos="cursos"
      :curso="curso"
      :evaluaciones="evaluaciones"
      :todasEvaluaciones="todasEvaluaciones"
      :promedioE="promedioE"
      :alumnos="alumnos"
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
      evaluacionesG: [],
      alumnos : [],
      promedioE: 0,
    };
  },
  async created() {
    this.findCurso();
    this.getEvaluations();
    this.getAllEvaluations();
    this.getAlumns();
  },
  mounted() {
    this.findCurso();
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
          this.promedioE = evaluaciones[0].promedio;
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