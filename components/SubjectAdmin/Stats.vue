<template>
  <v-container>
    <v-simple-table class="mb-20">
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left" v-for="item in head" :key="item.id">
              {{ item.text }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ prueba.minimo }}</td>
            <td>{{ prueba.maximo }}</td>
            <td>{{ prueba.promedio }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>
<script>
export default {
  props: ["prueba"],
  data() {
    return {
      head: [
        { text: "Nota mínima", value: "nota" },
        { text: "Nota máxima", value: "nota" },
        { text: "Promedio", value: "min" },
      ],
    };
  },
};
</script>