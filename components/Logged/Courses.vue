<template>
  <v-list-group :value="drop" prepend-icon="mdi-account-group">
    <template v-slot:activator>
      <v-list-item :to="link">
        <v-list-item-title>{{ name }}</v-list-item-title></v-list-item
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
</template>

<script>
export default {
  props: ["cursos","name","drop","link"],
  data: () => ({
    opciones: [
      ["Ver notas", "mdi-account-multiple-outline"],
      ["Ver fechas de evaluaciones", "mdi-cog-outline"],
    ]
  }),
  }
</script>