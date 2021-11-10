<template>
  <div>
    Tus cursos son : 
    <v-spacer></v-spacer>
    <CoursesCursos :cursos="cursos" />

  </div>
</template>
<script>
import Courses from "../../components/Courses/Cursos.vue";
export default {
  components: { Courses },
  layout: "logged",
  props: ['cursos'],
};
</script>