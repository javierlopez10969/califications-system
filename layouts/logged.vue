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
        <NuxtChild
          keep-alive
          :cursos="cursos"
          :registro="registro"
          :user="user"
          :semestre="semestre"
        />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span
        >&copy; {{ new Date().getFullYear()}}USACH</span
      >
    </v-footer>
  </v-app>
</template>

<script>
export default {
  created() {
    if (this.$auth.strategy.token.get() === null) {
      this.$router.push("/login");
    }
    this.getUserData();
    this.getHistoric();
  },
  methods: {
    async getUserData() {
      try {
        const res = await this.$axios.post(
          process.env.baseUrl + "users/getuser/",
          {
            token:this.$auth.strategy.token.get().slice(7),
          }
        );
        console.log(res.data);
        this.user = res.data.user;
        this.perfil = res.data.perfil;
        this.semestre = res.data.semester;
      } catch (error) {
        console.log(error.response.data.error);
        this.error = err.response.data.mensaje;
      }
    },
    async getHistoric() {
      try {
        const res = await this.$axios.post(
          process.env.baseUrl + "courses/list/",
          {
            token: this.$auth.strategy.token.get().slice(7),
            historic: true,
          }
        );
        var cursos = res.data.courses;
        this.registro = cursos;
        console.log(this.cursos);
        localStorage.setItem("registro", this.registro);
      } catch (error) {
        console.log(error);
        this.registro = [];
      }
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
      semestre: {},
      permisos: {},
      clipped: false,
      drawer: false,
      fixed: false,
    };
  },
};
</script>
