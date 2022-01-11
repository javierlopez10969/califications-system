<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" scrollable max-width="400px">
      <template #activator="{ on: onMenu }">
        <v-tooltip bottom>
          <template #activator="{ on: onTooltip }">
            <v-btn
              color="white"
              class="text--primary"
              fab
              v-on="{ ...onMenu, ...onTooltip }"
            >
              <v-icon>mdi-account-plus-outline</v-icon>
            </v-btn>
          </template>
          <span> Agregar alumno</span>
        </v-tooltip>
      </template>

      <v-card>
        <v-card-title>Seleccione a usuario agregar</v-card-title>
        <v-divider></v-divider>
        <v-card-text style="height: 300px"> 
            <SubjectAdminAlumnList :alumnos="alumnos" :modo="2" />
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      dialogm1: "",
      dialog: false,
      alumnos: [],
    };
  },
  created() {
    this.$axios
      .get(
        process.env.baseUrl +"courses/newalumns/" +
          this.$route.params.id +
          "/"
      )
      .then((res) => {
        var alumns = res.data.alumns;
        this.alumnos = alumns;
        console.log("ALUMNOS :" + this.alumnos);
      })
      .catch((error) => {
        console.log(error);
        this.registro = [];
      });
  },
};
</script>