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
        <!-- Perfil editable -->
        <v-list-item>
          <v-list-item-title>Mi perfil</v-list-item-title>
          <v-list-item-icon>
            <v-icon>mdi-account</v-icon>
          </v-list-item-icon>
        </v-list-item>
        <v-list-item to="/landing">
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Home</v-list-item-title>
        </v-list-item>
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
      <!-- Mis cursos-->
      <LoggedCourses :cursos="cursos" :name="'Cursos'" :drop="true" :link="'/cursos'"  />
      <!-- Registro -->
      <div v-if="registro !== []">
        <LoggedCourses :cursos="registro" :name="'Registro'" :drop="false" :link="'/registro'"  />
      </div>
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
        icon: "mdi-bookmark-multiple-outline",
        title: "Evaluaciones",
        to: "/evaluaciones",
      },
    ],
    user: {},
  }),
};
</script>