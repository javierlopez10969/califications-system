<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="RUT"
      :rules="rutRules"
      :counter="12"
      label="RUT"
      required
    ></v-text-field>
    <v-text-field type="password" label="Clave"></v-text-field>
    <v-btn href="/landing" class="text-center" rounded color="primary" dark block>
      Ingresar
    </v-btn>
    <v-spacer></v-spacer>
    <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
      Validate
    </v-btn>

    <v-btn color="error" class="mr-4" @click="reset"> Reset Form </v-btn>

    <v-btn color="warning" @click="resetValidation"> Reset Validation </v-btn>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    RUT: "",
    password: "",
    rutRules: [
      (v) => !!v || "Rut es necesario",
      (v) => v.length <= 12 || "Rut Incompleto",
    ],
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => v.length <= 10 || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+/.test(v) || "E-mail must be valid",
    ],
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
  },
};
</script>