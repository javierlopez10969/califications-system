<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-text-field
          v-model="evaluacion.name"
          :counter="10"
          label="Nombre evaluacion"
          required
        ></v-text-field>

        <v-text-field
          v-model="evaluacion.ponderation"
          label="Ponderacion"
          required
        ></v-text-field>
      </v-row>
    </v-container>
  </v-form>
</template>
<script>
export default {
  methods: {},
  data: () => ({
    valid: false,
    evaluacion: {
      name: "",
      ponderation: 0,
    },
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