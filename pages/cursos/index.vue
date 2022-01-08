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
  head: {
    title: "Mis cursos",
  },
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
          process.env.baseUrl + "courses/list/"
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