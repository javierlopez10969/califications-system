<template>
  <v-simple-table fixed-header height="300px">
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
</template>


<script>
export default {
  props: ["alumnos"],
};
</script>
