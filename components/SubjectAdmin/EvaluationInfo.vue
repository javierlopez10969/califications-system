<template>
  <v-container fluid>
    <v-form>
      <v-container>
        <v-col>
          <v-row>
            <h2 class="font-weight-bold text-h4 basil--text">
              Evaluación : {{ prueba.evaluacion.name }}
            </h2>
          </v-row>
          <v-row>
            <h2 class="font-weight-bold text-h5 basil--text">
              Fecha de evaluación : {{ prueba.evaluacion.evaluation_date }}
            </h2>
          </v-row>
          <v-row>
            <h2 class="font-weight-bold text-h5 basil--text">
              Ponderacion : {{ prueba.evaluacion.ponderation *100}} %
            </h2>
          </v-row>
          <v-row>
            <v-slider
              v-model="prueba.evaluacion.ponderation"
              :step="0.0001"
              :max="1"
              :min="0"
              label="Ponderacion"
            >
            </v-slider>
          </v-row>
          <v-row>
            {{ prueba.evaluacion.delivery_date }}
          </v-row>
          <v-row>
            {{ prueba.efective_delivery_date }}
          </v-row>
        </v-col>
      </v-container>
    </v-form>
  </v-container>
</template>
<script>
export default {
  props: ["prueba", "coordianciones"],
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