<template>
  <v-card>
    <v-card-title>
      Calificaciones de los alumnos
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Buscar..."
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="notas"
      class="elevation-1"
      :search="search"
    >
      <template v-slot:[`item.nota`]="{ item }">
        <v-chip :color="getColor(item.nota)" dark>
          <v-edit-dialog
            :return-value.sync="item.nota"
            large
            persistent
            @save="save"
            @cancel="cancel"
            @open="open"
            @close="close"
          >
            <div>{{ item.nota }}</div>
            <template v-slot:input>
              <div class="mt-4 text-h6">Cambiar nota</div>
              <v-text-field
                v-model="item.nota"
                :rules="notaRules"
                label="Edit"
                single-line
                counter
                autofocus
              ></v-text-field>
            </template>
          </v-edit-dialog>
        </v-chip>
      </template>
    </v-data-table>
    <v-snackbar v-model="snack" :timeout="3000" :color="snackColor">
      {{ snackText }}

      <template v-slot:action="{ attrs }">
        <v-btn v-bind="attrs" text @click="snack = false"> Close </v-btn>
      </template>
    </v-snackbar>
    <h5>{{ notaUpdate }}</h5>
  </v-card>
</template>
<script>
export default {
  props: ["notas"],
  data() {
    return {
      snack: false,
      notaUpdate: 0,
      snackColor: "",
      snackText: "",
      max25chars: (v) => v.length <= 25 || "Input too long!",
      search: "",
      notaRules: [
        (v) => !!v || "Nota requerida",
        (v) => (v >= 1 && v <= 7) || "La nota debe ser mayor que 1 y menor que 7",
      ],
      headers: [
        {
          text: "Nombre",
          align: "start",
          value: "perfil.first_name",
        },
        {
          text: "Apellido",
          align: "start",
          value: "perfil.last_name",
        },

        { text: "Notas", value: "nota" },
      ],
    };
  },
  methods: {
    getColor(nota) {
      if (nota > 3.9) return "blue";
      else return "red";
    },
    save() {
      this.snack = true;
      this.snackColor = "success";
      this.snackText = "Data saved";
    },
    cancel() {
      this.snack = true;
      this.snackColor = "error";
      this.snackText = "Canceled";
    },
    open() {
      this.snack = true;
      this.snackColor = "info";
      this.snackText = "Dialog opened";
    },
    close() {
      console.log("Dialog closed");
    },
  },
};
</script>