<template>
  <v-simple-table height="300px">
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Nombre</th>
          <th class="text-left">Calificación</th>
          <th class="text-left">Fecha de entrega</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in evaluaciones" :key="item.calificacion">
          <td>{{ item.nombre_evaluacion }}</td>
          <td>{{ item.calificacion }}</td>
           <td>{{ item.fecha_de_entrega }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
    props:["evaluaciones"],
  data() {
    return {
    };
  },
};
</script>