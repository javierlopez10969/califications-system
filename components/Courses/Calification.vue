<template>
  <v-container>
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
            <td>{{evaluacion.min}}</td>
            <td>{{evaluacion.max}}</td>
            <td>
              <v-icon
                @click="
                  obtenerApelacion(
                    evaluacion.id_calificacion,
                    evaluacion.nombre_evaluacion,
                    evaluacion.fecha_de_entrega
                  )
                "
                >mdi-information</v-icon
              >
            </td>
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
                    <v-list-item-subtitle>
                      {{ nombre_calificacion }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-content>
                    <v-list-item-title>Fecha</v-list-item-title>
                    <v-list-item-subtitle>
                      {{ fecha_calificacion }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item v-if="!existe_apelacion">
                  <v-list-item-content>
                    <v-list-item-title>
                      Apelar evaluacion
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
                        v-model="descripcionAp"
                        class="mb-0"
                      ></v-textarea>
                      <v-btn
                        class="mt-0"
                        outlined
                        x-small
                        color="primary"
                        @click="confirmar = true"
                        >Enviar</v-btn
                      >
                    </div>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item v-else>
                  <v-list-item-content>
                    <v-list-item-title v-if="apelacion_actual.answer === ''">Apelación en proceso</v-list-item-title>
                    <v-list-item-title v-else>Apelación Respondida</v-list-item-title>
                    <v-list-item-subtitle class="mb-1"
                      >Motivo:
                      {{ apelacion_actual.description }}</v-list-item-subtitle
                    >
                    <v-list-item-subtitle class="mb-1"
                      >Fecha:
                      {{ apelacion_actual.issue_date }}</v-list-item-subtitle
                    >
                    <div v-if="apelacion_actual.answer === ''">
                      <v-list-item-subtitle class="mb-1"
                        >Respuesta: Pendiente</v-list-item-subtitle
                      >
                    </div>
                    <dir v-else>
                      <v-list-item-subtitle class="mb-1"
                        >Respuesta:
                      </v-list-item-subtitle>
                      <v-textarea
                        filled
                        readonly
                        outlined
                        v-model="apelacion_actual.answer"
                      >
                      </v-textarea>
                    </dir>
                  </v-list-item-content>
                </v-list-item>

                <v-divider></v-divider>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="primary" text @click="cerrarAp"> Cerrar </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <v-dialog v-model="confirmar" persistent max-width="290">
      <v-card>
        <v-card-title class="text-h5"> Confirmar </v-card-title>
        <v-card-text>¿Está seguro que desea enviar esta apelación?</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="confirmar = false">
            Cancelar
          </v-btn>
          <v-btn color="green darken-1" text @click="crearApelacion">
            Aceptar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  props: ["evaluaciones"],
  data: () => ({
    id_calificacion: null,
    nombre_calificacion: null,
    fecha_calificacion: null,
    headers: [
      { text: "Evaluación", value: "nota" },
      { text: "Mi nota", value: "nota" },
      { text: "Nota mínima", value: "min" },
      { text: "Nota máxima", value: "max" },
      { text: "", value: "prom" },
    ],
    apelacion: {
      calification: 0,
      description: "",
      issue_date: null,
    },
    apelacion_actual: null,
    dialog: false,
    confirmar: false,
    descripcionAp: "",
    mostrarAp: false,
    existe_apelacion: false,
  }),
  methods: {
    cerrarAp() {
      this.mostrarAp = false;
      this.dialog = false;
      this.descripcionAp = "";
    },
    crearApelacion() {
      var apelacion = {
        calification: this.id_calificacion,
        description: this.descripcionAp,
        issue_date: "2022-01-19",
      };
      this.confirmar = false;
      this.mostrarAp = false;
      this.dialog = false;
      console.log(apelacion);
      this.$axios
        .post("appeals/detail/1/", apelacion)
        .then((res) => {
          alert("Apelacion creada");
        })
        .catch((error) => {
          alert(res.error);
          console.log(error);
        });
    },
    obtenerApelacion(id_calificacion, nombre_evaluacion, fecha_de_entrega) {
      this.nombre_calificacion = nombre_evaluacion;
      this.fecha_calificacion = fecha_de_entrega;
      this.id_calificacion = id_calificacion;
      this.dialog = true;
      this.$axios
        .get(process.env.baseUrl + "appeals/detail/" + id_calificacion + "/")
        .then((res) => {
          var apelacion = res.data;
          this.apelacion_actual = apelacion;
          this.existe_apelacion = apelacion.issue_date;
          console.log(apelacion);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>