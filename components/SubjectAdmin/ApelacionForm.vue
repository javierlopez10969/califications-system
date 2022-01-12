<template>
  <v-container fluid>
    <v-form
      ref="form"
      class="form-signin"
      lazy-validation
      @submit.prevent="responder"
    >
      <v-container fluid>
        <v-textarea
          disabled
          v-model="apelacion.description"
          filled
          auto-grow
          rows="1"
          row-height="15"
        >
          <template v-slot:label>
            <div>Apelación :</div>
          </template>
        </v-textarea>

        <v-textarea
          counter
          label="Respuesta"
          :rules="rules"
          v-model="apelacion.answer"
        ></v-textarea>
        <v-row class="justify-center">
          <v-btn
            type="submit"
            class="mb-10 mt-3 text-center justify-center"
            rounded
            color="secondary"
            >Responder
          </v-btn>
        </v-row>
      </v-container>
    </v-form>
    <v-snackbar v-model="snack" :timeout="3000" :color="snackColor">
      {{ snackText }}

      <template v-slot:action="{ attrs }">
        <v-btn v-bind="attrs" text @click="snack = false"> Cerrar </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
export default {
  props: ["apelacion"],

  methods: {
    async responder() {
      if (this.$refs.form.validate()) {
        try {
          await this.$axios.put("appeals/detail/1/", this.apelacion);
          this.snack = true;
          this.snackColor = "success";
          this.snackText = "Respondido";
        } catch (res) {
          this.snack = true;
          this.snackColor = "error";
          this.snackText = "Error al responder";
        }
      } else {
        this.snack = true;
        this.snackColor = "error";
        this.snackText = "Más de 10 caracteres";
      }
    },
  },
  data: () => ({
    snack: false,
    snackColor: "",
    snackText: "",
    valid: false,
    rules: [(v) => (v.length <= 100 && v.length > 10) || "Más de 10 caracters"],
    value: "Hello!",
  }),
};
</script>