<template>
  <v-app>
    <LoggedNavbar :cursos="cursos" />
    <v-main>
      <v-container>
        <NuxtChild :cursos="cursos" />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} USACH</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      cursos: [
        { ID: 1, nombre: "Calculo 1" },
        { ID: 2, nombre: "Algebra 1" },
        { ID: 3, nombre: "Fisica 1" },
        { ID: 4, nombre: "Taller de ingineria" },
      ],
      string: "Hello world",
    };
  },
};
</script>
