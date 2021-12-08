<template>
  <div>
    <v-list>
      <v-list>
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
      <v-list-group :value="true" prepend-icon="mdi-account-group">
        <template v-slot:activator>
          <v-list-item to="/cursos">
            <v-list-item-title>Mis cursos</v-list-item-title></v-list-item
          >
        </template>
        <!-- Curso-->
        <v-list-item v-for="(curso, i) in cursos" :key="i" link>
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>{{ curso.name }}</v-list-item-title>
              </v-list-item-content>
            </template>
            <!-- opciones-->
            <v-list-item v-for="([title, icon], i) in opciones" :key="i" link>
              <v-list-item-title v-text="title"></v-list-item-title>
              <v-list-item-icon>
                <v-icon v-text="icon"></v-icon>
              </v-list-item-icon>
            </v-list-item>
          </v-list-group>
        </v-list-item>
      </v-list-group>
      <!-- Registro -->
      <v-list-group :value="false" prepend-icon="mdi-account-group">
        <template v-slot:activator>
          <v-list-item to="/cursos">
            <v-list-item-title>Registro</v-list-item-title></v-list-item
          >
        </template>
        <!-- Curso-->
        <v-list-item v-for="(curso, i) in cursos" :key="i" link>
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>{{ curso.name }}</v-list-item-title>
              </v-list-item-content>
            </template>
            <!-- opciones-->
            <v-list-item v-for="([title, icon], i) in opciones" :key="i" link>
              <v-list-item-title v-text="title"></v-list-item-title>
              <v-list-item-icon>
                <v-icon v-text="icon"></v-icon>
              </v-list-item-icon>
            </v-list-item>
          </v-list-group>
        </v-list-item>
      </v-list-group>
    </v-list>
  </div>
</template>

<script>
export default {
  props: ["cursos", "registro"],
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
  }),
};
</script>