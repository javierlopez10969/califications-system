<template>
  <div>
    <CoursesCurso :cursos="cursos" :curso="curso" />
     <NuxtLink to="/cursos">Volver a mis cursos</NuxtLink>
    <SubjectAdminAlumnList :alumnos.sync="alumnos" />

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
      alumnos : [],
    };
  },
  mounted() {
    this.findCurso();
    this.getAlumns()
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
          console.log(alumns[0].email)
          console.log("ALUMNOS :" +this.alumnos);
        })
        .catch((error) => {
          console.log(error);
          this.registro = [];
        });
    },
  },
};
</script>
