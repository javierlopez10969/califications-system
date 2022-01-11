<template>
  <div>
    <v-card v-if="modo === 1">
      <v-card-title class="py-6">
        <h1 class="font-weight-bold text-h2 basil--text">Alumnos inscritos</h1>
        <v-spacer></v-spacer>
        <SubjectAdminInscriptionList />
      </v-card-title>
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
              <td><v-btn color="red"> Desinscribir</v-btn></td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
    <v-card v-if="modo === 2">
      <v-card-title class="py-6">
        {{ coordinaciones }}
        <v-select
          v-model="select"
          :hint="`${select.state}, ${select.abbr}`"
          :items="items"
          item-text="state"
          item-value="abbr"
          label="Select"
          persistent-hint
          return-object
          single-line
        ></v-select>
      </v-card-title>
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
              <td><v-btn color="green"> Agregar</v-btn></td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
  </div>
</template>


<script>
export default {
  props: ["alumnos", "modo"],
  data() {
    return {
      select: { state: "Florida", abbr: "FL" },
      items: [
        { state: "Florida", abbr: "FL" },
        { state: "Georgia", abbr: "GA" },
        { state: "Nebraska", abbr: "NE" },
        { state: "California", abbr: "CA" },
        { state: "New York", abbr: "NY" },
      ],
      coordinaciones: [],
    };
  },
  methods: {
    agregar() {},
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
