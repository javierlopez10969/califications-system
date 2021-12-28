<template>
  <v-container  fluid>
    <p class="text-h4 text--primary mb-0 text-left">Mi registro historico</p>
    <v-spacer></v-spacer>
    <v-col align="center">
      <CoursesCursos :cursos="registro" />
    </v-col>
  </v-container>
</template>
<script>
export default {
  layout: "logged",
  props: ["registro"],
};
</script>