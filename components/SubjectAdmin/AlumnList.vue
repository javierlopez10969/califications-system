<template>
  <v-card>
    <v-card-title class="text-center justify-center py-6">
      <h1 class="font-weight-bold text-h2 basil--text">Alumnos inscritos</h1>
      <!--
        <v-btn  dark color="indigo">
          <v-icon dark> mdi-plus </v-icon>
          Agregar evaluación
        </v-btn>-->
    </v-card-title>

    <v-simple-table fixed-header>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Correo del alumno</th>
            <th class="text-left">Desinscribir</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in alumnos" :key="item.id">
            <td>{{ item.email }}</td>
            <td><v-btn color="red"> Eliminar</v-btn></td>
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
