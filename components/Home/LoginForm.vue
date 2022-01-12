<template>
  <v-card width="500px" class="mx-auto mt-5 rounded-lg" elevation="12">
    <v-container class="pa-7">
      <v-card-title class="justify-center">
        <p class="text-h4 text--primary">Iniciar sesión</p>
      </v-card-title>

      <v-form
        ref="form"
        class="form-signin"
        lazy-validation
        @submit.prevent="userLogin"
      >
        <v-text-field
          v-model="user.username"
          :rules="emailRules"
          :prepend-icon="mdi - email"
          label="Correo institucional"
          required
        ></v-text-field>

        <v-text-field
          v-model="user.password"
          type="password"
          label="Clave"
          required
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
    valid: false,
    user: {
      username: "",
      password: "",
    },
    rutRules: [
      (v) => !!v || "Rut es necesario",
      (v) => v.length <= 12 || "Rut Incompleto",
    ],
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
  }),

  methods: {
    async userLogin() {
      if (this.$refs.form.validate()) {
        try {
          let response = await this.$auth.loginWith("local", {
            data: this.user,
          });
          this.$router.push({ path: "/landing" });
        } catch (err) {
          console.log(err);
          alert(err.response.data.error);
          console.log(err.response);
        }
      }
    },
  },
};
</script>