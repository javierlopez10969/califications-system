<template>
  <v-app>
    <LoggedNavbar
      :cursos="cursos"
      :user="user"
      :perfil="perfil"
      :registro="registro"
    />
    <v-main>
      <v-container>
        <NuxtChild :cursos="cursos" :registro="registro" :user="user" :semestre.sync="semestre" />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} USACH</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  created() {
    this.getUserData();
    this.getCourses();
    this.getHistoric();
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
        .post(process.env.baseUrl + "users/getuser/", {
          token: localStorage.getItem("token"),
        })
        .then(
          (res) => {
            //if successfull
            if (res.status === 200) {
              console.log(res.data);
              this.user = res.data.user;
              this.perfil = res.data.perfil;
              this.semestre= res.data.semester;
            }
          },
          (err) => {
            //alert(err.response.data.error);
            console.log(err.response.data.error);
            this.error = err.response.data.mensaje;
          }
        );
    },
    async getHistoric() {
      this.$axios
        .post(process.env.baseUrl + "courses/list/", {
          token: localStorage.getItem("token"),
          historic: true,
        })
        .then((res) => {
          var cursos = res.data.courses;
          this.registro = cursos;
          console.log(this.cursos);
        })
        .catch((error) => {
          console.log(error);
          this.registro = []
        });
    },
    async getCourses() {
      this.$axios
        .post(process.env.baseUrl + "courses/list/", {
          token: localStorage.getItem("token"),
        })
        .then((res) => {
          var cursos = res.data.courses;
          this.cursos = cursos;
          console.log(this.cursos);
        })
        .catch((error) => {
          this.cursos= []
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
      perfil: {},
      semestre : {},
      clipped: false,
      drawer: false,
      fixed: false,
    };
  },
};
</script>
