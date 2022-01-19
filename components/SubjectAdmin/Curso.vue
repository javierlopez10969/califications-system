<template>
  <v-container fluid>
    <v-card>
      <v-card-title class="py-6">
        <h4 class="font-weight-bold text-h5 basil--text">{{ curso.name }}</h4>
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
        <v-tab>
          <v-icon left> mdi-chart-box </v-icon>
          Stats
        </v-tab>

        <v-tab-item>
          <v-card>
            <!-- Las evaluaciones junto a las clasificaciones -->
            <v-card-text>
              <SubjectAdminEvaluations
                :curso="curso"
                :todasEvaluaciones="todasEvaluaciones"
                :promedioE="promedioE"
                :alumnos="alumnos"
                :coordinaciones="coordinaciones"
              />
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card>
            <v-card-text>
              <SubjectAdminAlumnList
                :alumnos="alumnos"
                :modo="1"
                :coordinaciones="coordinaciones"
              />
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card>
            <v-card-text>
              WENA PO
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs>
    </v-card>
  </v-container>
</template>

<script>
export default {
  props: [
    "curso",
    "evaluaciones",
    "todasEvaluaciones",
    "promedioE",
    "alumnos",
    "coordinaciones",
  ],
  data() {
    return {
      tab: null,
      text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    };
  },
};
</script>
