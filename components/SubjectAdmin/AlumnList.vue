<template>
  <div>
    <v-card v-if="modo === 1">
      <v-card-title class="py-6">
        <h1 class="font-weight-bold text-h2 basil--text">Alumnos inscritos</h1>
        <v-spacer></v-spacer>
        <SubjectAdminDialogButton
          :modo="`alumnos`"
          :icon="`mdi-account-plus-outline`"
          :span="`Agregar alumno`"
        />
      </v-card-title>
      <v-simple-table fixed-header>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">Nombre</th>
              <th class="text-left">RUT</th>
              <th class="text-left">Coordinacion</th>
              <th class="text-left">Aciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in alumnos" :key="item.id">
              <td>
                {{ item.profile.first_name }} {{ item.profile.last_name }}
              </td>
              <td>
                {{ item.profile.admision_date }}
              </td>
              <td>
                {{ item.coordination.name }} - {{ item.coordination.code }}
              </td>

              <td>
                <v-btn color="red" @click="desinscribir(item.coordination.id,item.id)"> Desinscribir</v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
    <v-card v-if="modo === 2">
      <v-card-title> Agrge a su alumno</v-card-title>
      <v-form>
        <v-select
          hint="Sección"
          v-model="select"
          :items="coordinaciones"
          :item-text="(item) => item.name + ' - ' + item.code"
          item-value="abbr"
          label="Seleccione la sección"
          persistent-hint
          return-object
          single-line
          required
        ></v-select>
        <v-simple-table fixed-header>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Nombre</th>
                <th class="text-left">Aciones</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in alumnos" :key="item.id">
                <td>
                  {{ item.profile.first_name }} {{ item.profile.last_name }}
                </td>
                <td>
                  <v-btn color="green" @click="agregar(select.id, item.id)">
                    Agregar</v-btn
                  >
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-form>
    </v-card>
  </div>
</template>


<script>
export default {
  props: ["alumnos", "modo"],
  data() {
    return {
      coordinaciones: [],
      select: [],
      valid: false,
    };
  },
  methods: {
    agregar(idCoord, idAlumno) {
      if (idCoord == undefined || idCoord == null) {
        alert("Seleccione una coordinacion");
      } else {
        this.$axios
          .post(
            process.env.baseUrl +
              "courses/usercordination/" +
              idCoord +
              "/" +
              idAlumno +
              "/"
          )
          .then((res) => {
            alert("Alumno agregado");
          })
          .catch((error) => {
            alert(error);
            console.log(error);
            this.coordinaciones = [];
          });
      }
    },
    desinscribir(idCoord, idAlumno) {
      if (idCoord == undefined || idCoord == null) {
        alert("Seleccione una coordinacion");
      } else {
        this.$axios
          .delete(
            process.env.baseUrl +
              "courses/usercordination/" +
              idCoord +
              "/" +
              idAlumno +
              "/"
          )
          .then((res) => {
            alert(res.data.message);
          })
          .catch((error) => {
            alert(error);
            console.log(error);
            this.coordinaciones = [];
          });
      }
    },
    getCoordinaciones() {
      this.$axios
        .get(
          process.env.baseUrl +
            "courses/coursecordination/" +
            this.$route.params.id +
            "/"
        )
        .then((res) => {
          this.coordinaciones = res.data.coordinaciones;
          console.log("COORDINACIONES ::::" + this.coordinaciones);
        })
        .catch((error) => {
          console.log(error);
          this.coordinaciones = [];
        });
    },
  },
  created() {
    this.getCoordinaciones();
  },
};
</script>
