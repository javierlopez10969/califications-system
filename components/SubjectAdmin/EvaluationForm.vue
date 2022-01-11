<template>
  <v-form v-model="valid" @submit.prevent="agregarEvaluacion()">
    <v-container>
      <v-col class="justify-center">
        <v-row>
          <v-text-field
            v-model="evaluacion.name"
            :counter="10"
            label="Nombre evaluacion"
            placeholder="PEP 1"
            required
          ></v-text-field>
        </v-row>

        <v-row>
          <v-text-field
            v-model="evaluacion.ponderation"
            label="Ponderacion"
            required
          ></v-text-field>
        </v-row>

        <v-row>
          <v-slider v-model="evaluacion.ponderation" label="Ponderacion">
          </v-slider>
        </v-row>
        <v-row>
          <v-select
            hint="Sección"
            v-model="select"
            :items="coordinaciones"
            :item-text="(item) => item.name + ' - ' + item.code"
            item-value="abbr"
            label="Seleccione la sección"
            persistent-hint
            return-object
            single-line
            required
          ></v-select>
        </v-row>
        <!--elgir la nota-->
        <v-row>
          {{ evaluacion.evaluation_date }}
          <v-menu
            v-model="menu2"
            :close-on-content-click="false"
            :nudge-right="40"
            transition="scale-transition"
            offset-y
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="evaluacion.evaluation_date"
                label="Picker without buttons"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="evaluacion.evaluation_date"
              @input="menu2 = false"
              color="secondary"
            ></v-date-picker>
          </v-menu>
        </v-row>
        <v-row class="justify-center">
          <v-btn
            type="submit"
            class="mb-10 mt-3 text-center justify-center"
            rounded
            color="secondary"
          >
            Agregar Nota
          </v-btn>
        </v-row>
      </v-col>
    </v-container>
  </v-form>
</template>
<script>
export default {
  props: ["coordinaciones"],
  methods: {
    agregarEvaluacion() {
      this.$axios
        .post(
          "evaluations/evaluation-list/",
          this.evaluacion
        )
        .then((res) => {
          var evaluaciones = res.data.evaluations;
          this.evaluaciones = evaluaciones;
          console.log(evaluaciones);
        })
        .catch((error) => {
          alert(error)
          console.log(error);
          this.registro = [];
        });
    },
  },
  data: () => ({
    valid: false,
    evaluacion: {
      name: "",
      ponderation: 0,
      evaluation_date: null,
      delivery_date: null,
      effective_delivery_date: null,
    },
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu: false,
    modal: false,
    menu2: false,
    nameRules: [
      (v) => !!v || "Name is required",
      (v) =>
        v.length <= 10 ||
        "El nombre de la evaluación debe ser de menos de 10 caracteres",
    ],
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+/.test(v) || "E-mail must be valid",
    ],
  }),
};
</script>