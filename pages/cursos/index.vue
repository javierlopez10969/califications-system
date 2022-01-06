<template>
  <v-container fill-height fluid>
    <v-col align="center">

      <CoursesCursos
        :cursos="cursos"
        :titulo="'Mis cursos  ' + semestre.semester + '-' + semestre.year"
      />
    </v-col>
  </v-container>
</template>
<script>
import Courses from "../../components/Courses/Cursos.vue";
export default {
  components: { Courses },
  layout: "logged",
  props: ["semestre"],
  ssr: false,
  data() {
    return {
      cursos: {},
    };
  },
  created() {
    this.getCourses();
  },
  methods: {
    async getCourses() {
      try {
        const res = await this.$axios.post(
          process.env.baseUrl + "courses/list/",
          { token: this.$auth.strategy.token.get().slice(7) }
        );
        var cursos = res.data.courses;
        this.cursos = cursos;
        console.log(this.cursos);
      } catch (error) {
        console.log(error);
        this.registro = [];
      }
    },
  },
};
</script>