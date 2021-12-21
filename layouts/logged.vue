<template>
  <v-app>
    <LoggedNavbar :cursos="cursos" :user="user" />
    <v-main>
      <v-container>
        <NuxtChild :cursos="cursos" :user.sync="user" />
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
    this.getUserData();
    this.getCourses();
  },
  async fetch() {},
  mounted: function () {
    if (localStorage.getItem("token") === null) {
      this.$router.push("/login");
    }
  },
  methods: {
    async getUserData() {
      this.$axios
        .post(process.env.baseUrl + "getuser/", {
          token: localStorage.getItem("token"),
        })
        .then(
          (res) => {
            //if successfull
            if (res.status === 200) {
              console.log(res.data);
              this.user = res.data.user;
              console.log(res.data.user)
            }
          },
          (err) => {
            //alert(err.response.data.error);
            console.log(err.response.data.error);
            this.error = err.response.data.mensaje;
          }
        );
    },
    async getCourses() {
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
  },
  data() {
    return {
      ip: 0,
      //Cursos actuales que cursa
      cursos: [],
      //Cursos de registro historico
      registro: [],
      //Usuario actual
      user: {},
      clipped: false,
      drawer: false,
      fixed: false,
    };
  },
};
</script>
