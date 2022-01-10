<template>
  <v-card width="500px" class="mx-auto mt-5 rounded-lg" elevation="12">
    <v-container class="pa-7">
      <v-card-title class="justify-center">
        <p class="text-h4 text--primary">Iniciar sesión</p>
      </v-card-title>

      <v-form
        ref="form"
        class="form-signin"
        @submit.prevent="userLogin"
        lazy-validation
      >
        <v-text-field
          v-model="user.username"
          :rules="emailRules"
          label="Correo institucional"
          required
        ></v-text-field>

        <v-text-field
          v-model="user.password"
          type="password"
          label="Clave"
        ></v-text-field>
        <v-btn
          type="submit"
          class="mb-10 mt-3 text-center"
          rounded
          color="secondary"
          light
          block
        >
          Ingresar
        </v-btn>
      </v-form>
    </v-container>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    user: {
      username: "",
      password: "",
    },
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
    async userLogin() {
      try {
        let response = await this.$auth.loginWith("local", {
          data: this.user,
        });
        console.log(response);
        this.$router.push({ path: "/landing" });
      } catch (err) {
        console.log(err);
        alert(err.response.data.status);
        console.log(err.response);

      }
    },
  },
};
</script>