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
        <v-chip :color="getColor(item.nota.value)" dark>
          <v-edit-dialog
            :return-value.sync="item.nota"
            large
            :persistent="true"
            :cancel-text="`Cancelar`"
            :save-text="`Guardar`"
            @save="save(item.nota)"
            @cancel="cancel"
            @open="open"
            @close="close"
          >
            <div>{{ item.nota.value }}</div>
            <template v-slot:input>
              <v-form ref="form" lazy-validation>
                <div class="mt-4 text-h6">Cambiar nota</div>
                <v-text-field
                  v-model="item.nota.value"
                  :rules="notaRules"
                  label="Edit"
                  single-line
                  counter
                  autofocus
                  required
                ></v-text-field>
              </v-form>
            </template>
          </v-edit-dialog>
        </v-chip>
      </template>
      <template v-slot:[`item.apelacion`]="{ item }">
        <SubjectAdminDialogButton
          v-if="item.apelacion.calification"
          :modo="`apelacion`"
          :icon="`mdi-information-outline`"
          :span="`Ver apelación`"
          :coordinaciones="coordinaciones"
          :apelacion="item.apelacion"
        />
        <v-tooltip v-else bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn icon v-bind="attrs" v-on="on">
              <v-icon color="grey lighten-1"> mdi-information-outline </v-icon>
            </v-btn>
          </template>
          <span>Sin apelación</span>
        </v-tooltip>
      </template>
    </v-data-table>
    <v-snackbar v-model="snack" :timeout="3000" :color="snackColor">
      {{ snackText }}

      <template v-slot:action="{ attrs }">
        <v-btn v-bind="attrs" text @click="snack = false"> Cerrar </v-btn>
      </template>
    </v-snackbar>
  </v-card>
</template>
<script>
export default {
  props: ["notas", "coordinaciones"],
  data() {
    return {
      snack: false,
      snackColor: "",
      snackText: "",
      max25chars: (v) => v.length <= 25 || "Input too long!",
      search: "",
      notaRules: [
        (v) => !!v || "Nota requerida",
        (v) =>
          (v >= 1 && v <= 7) || "La nota debe ser mayor que 1 y menor que 7",
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
        { text: "Calificaión", align: "start", value: "nota" },

        {
          text: "Fecha efectiva de entrega",
          value: "nota.efective_delivery_date",
        },

        { text: "Apelación", value: "apelacion" },
      ],
    };
  },
  methods: {
    updateNota(calificacion) {
      const today = new Date();
      const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
      calificacion['efective_delivery_date'] = date;
      this.$axios
        .put(
          "evaluations/edit/calification/" +
            this.$route.params.id +
            "/" +
            calificacion.id +
            "/",
          { calificacion: calificacion }
        )
        .then((res) => {
          this.$nuxt.refresh();
        })
        .catch((error) => {
          alert(error.data.message);
          console.log(error);
        });
    },
    getColor(nota) {
      if (nota > 3.9) return "blue";
      else return "red";
    },
    save(calificacion) {
      if (this.$refs.form.validate()) {
        this.snack = true;
        this.snackColor = "success";
        this.snackText = "Nota guardada";
        this.updateNota(calificacion);
        this.$nuxt.refresh();
      } else {
        this.snack = true;
        this.snackColor = "error";
        this.snackText = "Es necesario una nota en los rangos";
        this.$nuxt.refresh();
      }
    },
    cancel() {
      this.snack = true;
      this.snackColor = "error";
      this.snackText = "Canceled";
    },
    open() {
      this.snack = true;
      this.snackColor = "info";
      this.snackText = "Editando nota";
    },
    close() {
      console.log("Dialog closed");
    },
  },
};
</script>