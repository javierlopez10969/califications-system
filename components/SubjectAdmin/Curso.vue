<template>
  <v-container fluid>
    <v-card>
      <v-card-title class="text-center justify-center py-6">
        <h1 class="font-weight-bold text-h2 basil--text">{{curso.name}}</h1>
        <!--
        <v-btn  dark color="indigo">
          <v-icon dark> mdi-plus </v-icon>
          Agregar evaluación
        </v-btn>-->
      </v-card-title>
      <v-tabs
        v-model="tab"
        background-color="#023D8B"
        centered
        dark
        icons-and-text
      >
        <v-tabs-slider></v-tabs-slider>
        <v-tab>
          <v-icon left> mdi-note-edit-outline </v-icon>
          Evaluaciones
        </v-tab>
        <v-tab>
          <v-icon left> mdi-account-group </v-icon>
          Alumnos
        </v-tab>

        <v-tab-item>
          <v-card flat>
            <v-card-text>
              <SubjectAdminAdm
                :curso="curso"
                :todasEvaluaciones="todasEvaluaciones"
                :promedioE="promedioE"
                :alumnos="alumnos"
              />
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <v-card-text>
              <SubjectAdminAlumnList :alumnos="alumnos" />
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <v-card-text> </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs>
    </v-card>
  </v-container>
</template>

<script>
export default {
  props: ["curso", "evaluaciones", "todasEvaluaciones", "promedioE", "alumnos"],
  data() {
    return {
      tab: null,
      text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    };
  },
};
</script>

style: {

}