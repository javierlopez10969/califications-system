<template>
  <v-container class="pa-5">
    <v-row class="mb-20">
      <v-col>
        <p class="text-h4 mb-1 text-left">Datos del curso</p>
        <v-divider> </v-divider>
        <v-container class="pa-0">
          <v-list two-line class="pa-2">
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
            </v-list-item-group>
          </v-list>
        </v-container>
      </v-col>
      <v-col>
        <p class="text-h4 mb-1 text-left">Notas</p>
        <v-divider> </v-divider>
        <v-container class="pa-0 mt-4">
          <RegistroCalifications :evaluaciones = "evaluaciones"/>
        </v-container>
      </v-col>
    </v-row>

    <v-row class="text-center pa-15">
      <v-btn outlined depressed block small @click="volver">
        Volver a cursos
      </v-btn>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: ["curso","evaluaciones", "fecha"],
  data: () => ({
    items: [
      { header: "Today" },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
        title: "Brunch this weekend?",
        subtitle: `<span class="font-weight-bold">Ali Connors</span> &mdash; I'll be in your neighborhood doing errands this weekend. Do you want to hang out?`,
      },
      { divider: true, inset: true },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
        title: 'Summer BBQ <span class="grey--text text--lighten-1">4</span>',
        subtitle: `<span class="font-weight-bold">to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this weekend.`,
      },
      { divider: true, inset: true },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
        title: "Oui oui",
        subtitle:
          '<span class="font-weight-bold">Sandra Adams</span> &mdash; Do you have Paris recommendations? Have you ever been?',
      },
    ],
    headers: [
      {
        text: "Evaluación",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Mi nota", value: "nota" },
      { text: "Nota mínima", value: "min" },
      { text: "Nota máxima", value: "max" },
      { text: "Promedio", value: "prom" },
      { text: "Obs", value: "obs" },
    ],
    desserts: [
      {
        name: "Pep 1",
        nota: "1.0",
        min: "1.0",
        max: "1.0",
        prom: "1.0",
        obs: "pendiente",
      },
      {
        name: "Pep 2",
        nota: "1.0",
        min: "1.0",
        max: "1.0",
        prom: "1.0",
        obs: "pendiente",
      },
      {
        name: "Pep 3",
        nota: "1.0",
        min: "1.0",
        max: "1.0",
        prom: "1.0",
        obs: "pendiente",
      },
    ],
  }),
  methods: {
    volver() {
      this.$router.go(-1);
    },
  },
};
</script>