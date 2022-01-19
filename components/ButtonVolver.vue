<template>
  <v-row>
    <v-btn outlined depressed small @click="volver" color="secondary">
      <v-icon dark left> mdi-arrow-left</v-icon>
      {{text}}
    </v-btn>
  </v-row>
</template>

<script>
export default {
  props: ["text"],
  methods: {
    volver() {
      this.$router.go(-1);
      this.$nuxt.refresh();
    },
  },
};
</script>