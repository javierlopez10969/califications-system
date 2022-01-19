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
          :prepend-icon="`mdi-email`"
          label="Correo institucional"
          required
          :placeholder="'nombre.apellido@usach.cl'"
        ></v-text-field>

        <v-text-field
          v-model="user.password"
          type="password"
          label="Contraseña"
          required
          :prepend-icon="'mdi-key'"
          :rules="passwordRules"
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
  data: () => ({
    snack: false,
    snackColor: "",
    snackText: "",
    valid: false,
    user: {
      username: "",
      password: "",
    },
    rutRules: [
      (v) => !!v || "Rut es necesario",
      (v) => v.length <= 12 || "Rut Incompleto",
    ],
    passwordRules: [
      (v) => !!v || "Contraseña necesaria",
      (v) => v.length >= 8 || "Contraseña incorrecta",
    ],
    emailRules: [
      (v) => !!v || "El correo es requerido",
      (v) => /.+@.+\..+/.test(v) || "El correo debe ser valido",
    ],
  }),

  methods: {
    async userLogin() {
      if (this.$refs.form.validate()) {
        try {
          let response = await this.$auth.loginWith("local", {
            data: this.user,
          });

          this.snack = true;
          this.snackColor = "succes";
          this.snackText = "Ingreso exitoso";
          this.$router.push({ path: "/landing" });
        } catch (err) {
          console.log(err);
          console.log(err.response);
          this.snack = true;
          this.snackColor = "error";
          this.snackText = "Usuario o contraseñas incorrectas";
        }
      } else {
        this.snack = true;
        this.snackColor = "error";
        this.snackText = "Ingrese los datos necesarios por favor";
      }
    },
  },
};
</script>