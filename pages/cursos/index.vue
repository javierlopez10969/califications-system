<template>
  <div>
    Tus cursos son : 
    <v-spacer></v-spacer>
    <LoggedCourses :cursos="cursos" />

  </div>
</template>
<script>
import Courses from "../../components/Logged/Courses.vue";
export default {
  components: { Courses },
  layout: "logged",
  props: ['cursos'],
};
</script>