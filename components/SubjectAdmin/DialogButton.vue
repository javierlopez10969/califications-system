<template>
  <div>
    <!-- Caso agregar alumno-->
    <v-dialog
      v-if="modo === `alumnos`"
      v-model="dialog"
      scrollable
      max-width="400px"
    >
      <template #activator="{ on: onMenu }">
        <v-tooltip bottom>
          <template #activator="{ on: onTooltip }">
            <v-btn
              color="white"
              class="text--primary"
              fab
              v-on="{ ...onMenu, ...onTooltip }"
            >
              <v-icon> {{ icon }} </v-icon>
            </v-btn>
          </template>
          <span> {{ span }}</span>
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

    <!-- Caso agregar evaluacion-->
    <v-dialog
      v-if="modo === `evaluacion`"
      v-model="dialog"
      scrollable
      max-width="400px"
    >
      <template #activator="{ on: onMenu }">
        <v-tooltip bottom>
          <template #activator="{ on: onTooltip }">
            <v-btn
              color="white"
              class="text--primary"
              fab
              v-on="{ ...onMenu, ...onTooltip }"
            >
              <v-icon> {{ icon }} </v-icon>
            </v-btn>
          </template>
          <span> {{ span }}</span>
        </v-tooltip>
      </template>

      <v-card>
        <v-card-title>Seleccione a usuario agregar</v-card-title>
        <v-divider></v-divider>
        <v-card-text style="height: 300px">
          <SubjectAdminEvaluationForm />
        </v-card-text>
        <v-divider></v-divider>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: ["modo", "icon", "span"],
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
        process.env.baseUrl + "courses/newalumns/" + this.$route.params.id + "/"
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