<template>
  <div>
    <v-app-bar dense>
      <v-btn href="/" icon>
        <v-icon>mdi-home</v-icon>
      </v-btn>

      <v-toolbar-title>Sistema de notas</v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn to="/login" rounded color="primary" dark> Iniciar Sesión </v-btn>
      <v-menu left bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </div>
</template>
<script>
export default {

};
</script>
