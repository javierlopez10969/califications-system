<template>
  <v-container fluid>
    <v-card color="basil">
      <v-card-title class="text-center justify-center py-6">
        <h1 class="font-weight-bold text-h2 basil--text">Evaluaciones</h1>
      </v-card-title>

      <v-tabs v-model="tab" background-color="transparent" color="basil" grow>
        <v-tab v-for="prueba in todasEvaluaciones" :key="prueba.id">
          {{ prueba.evaluacion }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tab">
        <v-tab-item v-for="prueba in todasEvaluaciones" :key="prueba.id">
          <v-card color="basil" flat>
            <!--Contenido-->
            <v-card-text>
              <!--TAB VERTICAL-->
              <v-tabs vertical>
                <v-tab v-for="seccion in head3" :key="seccion">
                  {{ seccion.text }}
                </v-tab>

                <v-tab-item>
                  <!-- Tabla de notas-->
                  <v-simple-table class="mb-20">
                    <template v-slot:default>
                      <thead>
                        <tr>
                          <th
                            class="text-left"
                            v-for="item in head"
                            :key="item.id"
                          >
                            {{ item.text }}
                          </th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="notas in prueba.notas" :key="notas.id">
                          <td>{{ notas.usuario }}</td>
                          <!-- notas rojas en rojo-->
                          <td>
                            <v-chip :color="getColor(notas.nota)" dark>
                              {{ notas.nota }}
                            </v-chip>
                          </td>
                          <td>-</td>
                        </tr>
                      </tbody>
                    </template>
                  </v-simple-table>
                </v-tab-item>
                <v-tab-item>
                  <!-- Tabla de estadisticas-->
                  <v-simple-table class="mb-20">
                    <template v-slot:default>
                      <thead>
                        <tr>
                          <th
                            class="text-left"
                            v-for="item in head2"
                            :key="item.id"
                          >
                            {{ item.text }}
                          </th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr>
                          <td>{{ prueba.minimo }}</td>
                          <td>{{ prueba.maximo }}</td>
                          <td>{{ prueba.promedio }}</td>
                        </tr>
                      </tbody>
                    </template>
                  </v-simple-table>
                </v-tab-item>
                <v-tab-item>
                  <!-- Tabla de alumnos-->
                </v-tab-item>
              </v-tabs>
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
export default {
  props: ["curso", "evaluaciones", "todasEvaluaciones", "promedioE", "alumnos"],
  data() {
    return {
      tab: null,
      items: ["Appetizers", "Entrees", "Deserts", "Cocktails"],
      head: [
        { text: "Estudiante", value: "nota" },
        { text: "Nota", value: "nota" },
        { text: "Observación", value: "min" },
      ],
      head2: [
        { text: "Nota mínima", value: "nota" },
        { text: "Nota máxima", value: "nota" },
        { text: "Promedio", value: "min" },
      ],
      head3: [
        { text: "Notas", value: "nota" },
        { text: "Estadisticas", value: "nota" },
        { text: "Alumnos", value: "min" },
      ],
      text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    };
  },
  methods: {
    getColor(nota) {
      if (nota > 3.9) return "blue";
      else return "red";
    },
  },
};
</script>

<style>
/* Helper classes */
.basil {
  background-color: #ffffff !important;
}
.basil--text {
  color: #356859 !important;
}
</style>