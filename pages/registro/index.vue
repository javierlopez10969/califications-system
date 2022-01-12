<template>
  <v-container fill-height fluid>
    <v-container v-if="registro.length === 0">
      <p class="text-h4 text--primary mb-0 text-left">Sin cursos.</p>
    </v-container>
    <v-container v-else>
      <RegistroCursos :cursos="registro" />
    </v-container>
  </v-container>
</template>
<script>
export default {
  layout: "logged",
  props: ["registro"],
};
</script>