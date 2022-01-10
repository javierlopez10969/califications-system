<template>
  <v-card>
    <v-card-title class="py-6">
      <h1 class="font-weight-bold text-h2 basil--text">Alumnos inscritos</h1>
      <v-spacer></v-spacer>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="white"
            class="text--primary"
            fab
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </template>
        <span> Agregar alumno</span>
      </v-tooltip>
    </v-card-title>

    <v-simple-table fixed-header>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Nombre</th>
            <th class="text-left">Aciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in alumnos" :key="item.id">
            <td>{{ item.profile.first_name }} {{ item.profile.last_name }}</td>
            <td><v-btn color="red"> Desinscribir</v-btn></td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-card>
</template>


<script>
export default {
  props: ["alumnos"],
};
</script>
