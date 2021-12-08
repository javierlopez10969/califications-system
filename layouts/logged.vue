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
  created: function () {
    console.log("API URL :" + process.env.baseUrl);
    this.$axios
      .get(process.env.baseUrl + "courses/")
      .then((res) => {
        var cursos = res.data;
        this.cursos = cursos;
        console.log(this.cursos);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  data() {
    return {
      ip: 0,
      cursos: [],
      clipped: false,
      drawer: false,
      fixed: false,
    };
  },
};
</script>
