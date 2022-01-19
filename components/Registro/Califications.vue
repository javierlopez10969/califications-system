<template>
  <v-card>
    <v-card-title>Mis Calificaciones </v-card-title>
    <v-data-table
      :headers="headers"
      :items="evaluaciones"
      class="elevation-1"
      hide-default-footer
    >
      <template v-slot:[`item.calificacion`]="{ item }">
        <v-chip :color="getColor(item.calificacion)" class="white--text">
          {{ item.calificacion }}
        </v-chip>
      </template>
    </v-data-table>
  </v-card>
</template>
<script>
export default {
  props: ["evaluaciones", "fecha"],
  data() {
    return {
      snack: false,
      snackColor: "",
      snackText: "",
      max25chars: (v) => v.length <= 25 || "Input too long!",
      search: "",
      headers: [
        {
          text: "Evaluacion",
          align: "start",
          value: "nombre_evaluacion",
        },
        { text: "Nota", value: "calificacion" },
      ],
    };
  },
  methods: {
    getColor(nota) {
      if (nota > 3.9) return "blue";
      else return "red";
    },
  },
};
</script>