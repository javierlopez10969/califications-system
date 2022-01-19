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
              <div class="chart">
                    <SubjectAdminChart :data="barChartData" :options="barChartOptions" :height="200"/>
              </div>
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
      datos_grafico: null,
      barChartData: {
        labels: [],
        datasets: [
          {
            label: "Visualizaciones",
            data:   [ 5.5, 3, 6.9, 5.1 ],
            backgroundColor: "rgba(20, 255, 0, 0.3)",
            borderColor: "rgba(100, 255, 0, 1)",
            borderWidth: 2,
          },
        ],
      },
      barChartOptions: {
        responsive: true,
        legend: {
          display: false,
        },
        title: {
          display: true,
          text: "Google analytics data",
          fontSize: 24,
          fontColor: "#6b7280",
        },
        tooltips: {
          backgroundColor: "#17BF62",
        },
        scales: {
          xAxes: [
            {
              gridLines: {
                display: true,
              },
            },
          ],
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
                max: 7,
                min: 1,
                stepSize: 1,
              },
              gridLines: {
                display: true,
              },
            },
          ],
        },
      },
    };
  },
  methods: {
     async obtenerDatosGrafico(){
         this.$axios
        .get(
          process.env.baseUrl +
            "evaluations/grafico/2" +
            "/"
        )
        .then((res) => {
          this.datos_grafico = res.data;
          this.barChartData.labels = this.datos_grafico.alumnos;
          this.barChartData.datasets.data = this.datos_grafico.notas;
          console.log(this.barChartData.datasets.data)
        })
        .catch((error) => {
          console.log(error);
        });
     }
  },
  mounted() {
      this.obtenerDatosGrafico();
  },
};
</script>
