<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <LoggedSidebar
        :cursos="cursos"
        :registro="registro"
        :user.sync="user"
        :perfil.sync="perfil"
      />
    </v-navigation-drawer>
    <v-app-bar dense :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />

      <v-spacer />

      <v-spacer></v-spacer>

      <LoggedNotification />
      <v-btn @click="userLogout" rounded color="red">
        Cerrar sesión</v-btn
      >

    </v-app-bar>
  </div>
</template>
<script>
import Notification from "./Notification.vue";
export default {
  props: ["cursos", "user", "registro", "perfil"],
  components: { Notification },
  data() {
    return {
      clipped: true,
      drawer: true,
      fixed: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Sistema de notas",
    };
  },
  methods: {
    async userLogout() {
      try {
        console.log("LOGOUT");
        let response = await this.$auth.logout("local");
        this.$router.push({ path: "/login" });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
