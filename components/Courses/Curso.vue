<template>
    <v-container class="pa-5">
        <!-- Caso de alumnos-->
        <v-row class="mb-20" v-if="todasEvaluaciones.length === 0">
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
                                    <p class="text-h5">{{curso.name}}</p>
                                </v-list-item-subtitle>
                            </v-list-item-content>
                            <v-list-item-content>
                                <v-list-item-title>
                                    <p class="text-h6 font-weight-bold mb-0">Descripción de la asignatura</p>
                                </v-list-item-title>
                                <v-list-item-subtitle v-if="curso.description != ''">
                                    <p class="text-h5">{{curso.description}}</p>
                                </v-list-item-subtitle>
                                <v-list-item-subtitle v-else>Sin descripción.</v-list-item-subtitle>
                            </v-list-item-content>
                            <v-list-item-content>
                                <v-list-item-title>
                                    <p class="text-h6 font-weight-bold mb-0">Promedio</p>
                                </v-list-item-title>
                                <v-list-item-subtitle v-if="promedioE!==0">
                                    <p class="text-h5">{{promedioE}}</p>
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
                            <th class="text-left" v-for="item in headers" :key="item.id">{{item.text}}</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="evaluacion in evaluaciones" :key="evaluacion.id">
                            <td>{{ evaluacion.nombre_evaluacion }}</td>
                            <td>{{ evaluacion.calificacion }}</td>
                            <td>1.0</td>
                            <td>7.0</td>
                            <td>4.0</td>
                            <td>{{ evaluacion.fecha_de_entrega }}</td>
                        </tr>
                        </tbody>
                    </template>
                </v-simple-table>
            </v-col>
        </v-row>
        <!-- Caso Profesor-->
        <v-row v-else>
            <SubjectAdminEvaluations :curso="curso" :todasEvaluaciones="todasEvaluaciones" :promedioE="promedioE" />
        </v-row>
        
        <v-row class="pa-10">
            <v-btn outlined depressed small @click="volver">
                <v-icon dark left> mdi-arrow-left</v-icon>
                Volver a cursos
            </v-btn>
        </v-row>
    </v-container>

</template>

<script>
export default {
  props : ["curso", "evaluaciones", "todasEvaluaciones", "promedioE"],
    data: () => ({
      headers: [
          { text: 'Evaluación', value: 'nota' },
          { text: 'Mi nota', value: 'nota' },
          { text: 'Nota mínima', value: 'min' },
          { text: 'Nota máxima', value: 'max' },
          { text: 'Promedio', value: 'prom' },
          { text: 'Fecha', value: 'prom' },
        ],
        head: [
          { text: 'Estudiante', value: 'nota' },
          { text: 'Nota', value: 'nota' },
          { text: 'Observación', value: 'min' },
        ],
        head2: [
          { text: 'Nota mínima', value: 'nota' },
          { text: 'Nota máxima', value: 'nota' },
          { text: 'Promedio', value: 'min' },
        ],
    }),
    methods: {
        volver(){
            this.$router.go(-1)
        },
    }
}
</script>