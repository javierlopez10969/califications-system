<!--componente curso solo para el caso alumno-->
<template>
  <v-container class="pa-5">
    <!-- Caso de alumnos-->
    <v-row class="mb-20">
      <v-col cols="5">
        <p class="text-h4 mb-1 text-left">Datos del curso</p>
        <v-divider> </v-divider>
        <v-container class="pa-0">
          <v-list class="pa-2">
            <v-list-item-group two-line>
              <v-list-item-content>
                <v-list-item-title>
                  <p class="text-h6 font-weight-bold mb-0">Asignatura</p>
                </v-list-item-title>
                <v-list-item-subtitle>
                  <p class="text-h5">{{ curso.name }}</p>
                </v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-title>
                  <p class="text-h6 font-weight-bold mb-0">
                    Descripción de la asignatura
                  </p>
                </v-list-item-title>
                <v-list-item-subtitle v-if="curso.description != ''">
                  <p class="text-h5">{{ curso.description }}</p>
                </v-list-item-subtitle>
                <v-list-item-subtitle v-else
                  >Sin descripción.</v-list-item-subtitle
                >
              </v-list-item-content>
              <v-list-item-content>
                <v-list-item-title>
                  <p class="text-h6 font-weight-bold mb-0">Promedio</p>
                </v-list-item-title>
                <v-list-item-subtitle v-if="promedioE !== 0">
                  <p class="text-h5">{{ promedioE }}</p>
                </v-list-item-subtitle>
                <v-list-item-subtitle v-else>
                  <p class="text-h5">Sin notas.</p>
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item-group>
          </v-list>
        </v-container>
      </v-col>
      <v-col>
        <p class="text-h4 mb-1 text-left">Notas</p>
        <v-divider> </v-divider>
        <CoursesCalification :evaluaciones="evaluaciones" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: ["curso", "evaluaciones", "todasEvaluaciones", "promedioE", "alumnos"],
};
</script>