<template>
  <div class="text-center">
    Bienvenido al sistema de notas
    <CoursesGraphic />
    <v-btn class="ma-2" outlined color="indigo"> Outlined Button </v-btn>
    <v-btn class="ma-2" outlined fab color="teal">
      <v-icon>mdi-format-list-bulleted-square</v-icon>
    </v-btn>
    <v-btn class="ma-2" outlined large fab color="indigo">
      <v-icon>mdi-pencil</v-icon>
    </v-btn>
  </div>
</template>
<script>
export default {
  layout: "logged",
  props: [
    'cursos',
    'string'
  ]
};
</script>