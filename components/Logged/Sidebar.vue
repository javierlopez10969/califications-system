<template>
  <div>
    <v-list>
      <v-list>
        <!-- Perfil-->
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-list-item-avatar>
        </v-list-item>
        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="text-h6">
              {{ perfil.first_name }} {{ perfil.last_name }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action>
            <v-icon>mdi-menu-down</v-icon>
          </v-list-item-action>
        </v-list-item>
        <!--  editable -->
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-list>
  </div>
</template>

<script>
export default {
  props: ["cursos", "registro", "user", "perfil"],
  data: () => ({
    opciones: [
      ["Ver notas", "mdi-account-multiple-outline"],
      ["Ver fechas de evaluaciones", "mdi-cog-outline"],
    ],
    items: [
      {
        icon: "mdi-account",
        title: "Mi perfil",
        to: "",
      },
      {
        icon: "mdi-home",
        title: "Home",
        to: "/landing",
      },
      {
        icon: "mdi-calendar",
        title: "Evaluaciones",
        to: "/evaluaciones",
      },
      {
        icon: "mdi-school",
        title: "Mis cursos",
        to: "/cursos",
      },
      {
        icon: "mdi-archive",
        title: "Registro Historico",
        to: "/registro",
      },
      {
        icon: "mdi-cog",
        title: "Configuraciones",
        to: "",
      },
      {
        icon: "mdi-account-circle",
        title: "Salir",
        to: "",
      },
    ],
  }),
};
</script>