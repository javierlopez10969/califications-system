<!-- Componente que muestra las evaluaciones junto a las calificaciones-->
<template>
  <v-container fluid>
    <v-card color="basil">
      <v-card-title class="py-6">
        <h1 class="font-weight-bold text-h2 basil--text">Evaluaciones</h1>
        <v-spacer></v-spacer>

        <SubjectAdminDialogButton
          :modo="`evaluacion`"
          :icon="`mdi-plus`"
          :span="`Agregar Evaluación`"
        />

        <v-file-input accept="image/*" label="File input"></v-file-input>
      </v-card-title>
      <v-divider></v-divider>
      <v-spacer></v-spacer>
      <v-spacer></v-spacer>
      <v-spacer></v-spacer>
      <div v-if="todasEvaluaciones.length === 0">
        <h1 class="font-weight-bold text-h4 text-center basil--text">
          No hay evaluaciones
        </h1>
      </div>
      <v-tabs v-model="tab" background-color="transparent" color="basil" grow>
        <v-tab v-for="prueba in todasEvaluaciones" :key="prueba.id">
          {{ prueba.evaluacion.name }}
        </v-tab>
      </v-tabs>
      <v-tabs-items v-model="tab">
        <v-tab-item v-for="prueba in todasEvaluaciones" :key="prueba.id">
          <v-card color="basil" flat>
            <!--Contenido-->
            <v-card-text>
              <!--TAB VERTICAL-->
              <v-tabs vertical>
                <v-tab v-for="seccion in headTab" :key="seccion">
                  {{ seccion.text }}
                </v-tab>

                <!-- Tabla de notas-->
                <v-tab-item>
                  <SubjectAdminCalificationList :notas="prueba.notas" />
                </v-tab-item>

                <!-- Tabla de estadisticas-->
                <v-tab-item>
                  <SubjectAdminStats :prueba="prueba" />
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
  props: ["curso", "evaluaciones", "todasEvaluaciones", "promedioE"],
  data() {
    return {
      tab: null,
      items: ["Appetizers", "Entrees", "Deserts", "Cocktails"],
      headTab: [
        { text: "Notas", value: "nota" },
        { text: "Estadisticas", value: "nota" },
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
  color: #fa7f36 !important;
}
</style>