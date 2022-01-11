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
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left" v-for="item in headers" :key="item.id">
                  {{ item.text }}
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="evaluacion in evaluaciones" :key="evaluacion.id">
                <td>{{ evaluacion.nombre_evaluacion }}</td>
                <td>{{ evaluacion.calificacion }}</td>
                <td>1.0</td>
                <td>7.0</td>
                <td>4.0</td>
                <td><v-icon @click="dialog = true">mdi-information</v-icon></td>
                <v-dialog v-model="dialog" width="500">
                  <v-card>
                    <v-toolbar dark color="primary" class="mb-3">
                      <v-toolbar-title>Información adicional</v-toolbar-title>
                    </v-toolbar>

                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title
                          >Nombre de la evaluación</v-list-item-title
                        >
                        <v-list-item-subtitle>{{
                          evaluacion.nombre_evaluacion
                        }}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title>Fecha</v-list-item-title>
                        <v-list-item-subtitle>{{
                          evaluacion.fecha_de_entrega
                        }}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                    <v-list-item>
                      <v-list-item-content>
                        <v-list-item-title>
                          Apelar nota
                          <v-icon @click="mostrarAp = !mostrarAp"
                            >mdi-information</v-icon
                          >
                        </v-list-item-title>
                        <div v-if="mostrarAp">
                          <v-list-item-subtitle class="mb-2">
                            Motivo
                          </v-list-item-subtitle>
                          <v-textarea
                            outlined
                            :value="descripcionAp"
                            class="mb-0"
                          ></v-textarea>
                          <v-btn class="mt-0" outlined x-small color="primary"
                            >Enviar</v-btn
                          >
                        </div>
                      </v-list-item-content>
                    </v-list-item>
                    <v-divider></v-divider>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="primary" text @click="dialog = false">
                        Cerrar
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
    <div class="text-center"></div>
  </v-container>
</template>

<script>
export default {
  props: ["curso", "evaluaciones", "todasEvaluaciones", "promedioE", "alumnos"],
  data: () => ({
    headers: [
      { text: "Evaluación", value: "nota" },
      { text: "Mi nota", value: "nota" },
      { text: "Nota mínima", value: "min" },
      { text: "Nota máxima", value: "max" },
      { text: "Promedio", value: "prom" },
      { text: "", value: "prom" },
    ],
    dialog: false,
    descripcionAp: "",
    mostrarAp: false,
  }),
  methods: {
    volver() {
      this.$router.go(-1);
      this.$nuxt.refresh();
    },
  },
};
</script>