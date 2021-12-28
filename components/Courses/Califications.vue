<template>
  <div>
    <v-simple-table height="300px" v-if="!fecha">
      {{ fecha }}
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
    <v-simple-table height="300px" v-else>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Nombre</th>
            <th class="text-left">Fecha de evaluación</th>
            <th class="text-left">Fecha de entrega</th>
            <th class="text-left">Fecha de efectiva entrega</th>
            <th class="text-left">Ponderacion</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in evaluaciones" :key="item.calificacion">
            <td>{{ item.name }}</td>
            <td>{{ item.evaluation_date }}</td>
            <td>{{ item.delivery_date }}</td>
            <td>{{ item.efective_delivery_date }}</td>
            <td>{{ (item.ponderation * 100 ).toString() + "%"}}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  props: ["evaluaciones", "fecha"],
  data() {
    return {};
  },
};
</script>