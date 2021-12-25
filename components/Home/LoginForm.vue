<template>
        <v-card width="500px" class="mx-auto mt-5 rounded-lg"  elevation="12">
            <v-container class="pa-7">
                <v-card-title class="justify-center">
                    <p class="text-h4 text--primary">
                        Iniciar sesión
                    </p>
                </v-card-title>

                <v-form ref="form" class="form-signin" @submit.prevent="login" lazy-validation>
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
                    <v-btn type="submit" class="success mb-10 mt-3 text-center" rounded color="primary" dark block>
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
    login() {
      this.$axios.post(process.env.baseUrl + "users/login/", this.user).then(
        (res) => {
          //if successfull
          if (res.status === 200) {
            localStorage.setItem("token", res.data.token);
            console.log(res.data);
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