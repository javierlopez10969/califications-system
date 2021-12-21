<template>
  <v-form ref="form" class="form-signin" @submit.prevent="login" lazy-validation>
    <v-text-field
      v-model="user.username"
      :rules="emailRules"
      :counter="12"
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
      class="text-center"
      rounded
      color="primary"
      dark
      block
    >
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
    login() {
      this.$axios.post(process.env.baseUrl + "login/", this.user).then(
        (res) => {
          //if successfull
          if (res.status === 200) {
            localStorage.setItem("token", res.data.token);
            console.log(res.data)
            this.$router.push({ path: "/landing" });
          }
        },
        (err) => {
          alert(err.response.data.error);
          console.log(err.response);
          this.error = err.response.data.mensaje;
        }
      );
    },
  },
};
</script>