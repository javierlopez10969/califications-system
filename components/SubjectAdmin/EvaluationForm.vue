<template>
  <v-container class="pa-7">
    <v-form
      ref="form"
      class="form-signin"
      lazy-validation
      @submit.prevent="agregarEvaluacion"
    >
      <v-container>
        <v-col class="justify-center">
          <v-row>
            <v-text-field
              v-model="evaluacion.name"
              :counter="10"
              label="Nombre evaluacion"
              placeholder="PEP 1"
              :rules="nameRules"
              required
            ></v-text-field>
          </v-row>

          <v-row>
            <v-text-field
              v-model="evaluacion.ponderation"
              label="Ponderacion %"
              type="number"
              :rules="percentRules"
              required
            ></v-text-field>
          </v-row>

          <v-row>
            <v-slider v-model="evaluacion.ponderation" :step="0.01" label="Ponderacion">
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
                  label="Fecha de evaluaciones"
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
  </v-container>
</template>
<script>
export default {
  props: ["coordinaciones"],
  methods: {
    async agregarEvaluacion() {
      if (this.$refs.form.validate()) {
        try {
          this.evaluacion["coordination"] = this.select.id;
          this.evaluacion["ponderation"] = this.evaluacion["ponderation"]/100;
          res = await this.$axios.post("evaluations/evaluations-list/",this.evaluacion);

        } catch (err) {
          console.log(err);
          alert("F en el chat");
          console.log(err.response);
        }
      }
    },
  },
  data: () => ({
    valid: false,
    evaluacion: {
        "name": '',
        "evaluation_date": null,
        "delivery_date": null,
        "efective_delivery_date": null,
        "ponderation": 0.0,
    },
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu: false,
    modal: false,
    menu2: false,
    nameRules: [
      (v) => !!v || "Nombre es requirido",
      (v) =>
        v.length <= 10 ||
        "El nombre de la evaluación debe ser de menos de 10 caracteres",
    ],
    percentRules: [
      (v) => !!v || "Porcentaje requerido",
      (v) => ( v >= 0&& v <= 35 || "El porcentaje debe ser menor de 35 %"),
    ],
  }),
};
</script>