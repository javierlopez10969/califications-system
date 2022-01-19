<template>
  <v-container>
    <v-flex d-flex>
      <v-layout wrap>
        <v-flex v-for="(item, i) in cursos" :key="i">

            <p class="text-h4 text--primary mb-0 text-left">Semestre {{item.semester}}-{{item.year}}</p>
          <v-card class="mt-8 text-left" max-width="470" v-for="e in item.courses" :key="e.id">
            <v-img
              src="https://uvirtual.usach.cl/moodle/theme/image.php/eguru/theme/1640116840/cs02/no-image"
              height="150px"
            ></v-img>
            <v-card-title>
              {{ e.name}}
            </v-card-title>
            <v-card-actions>

              <div >
                <v-btn
                  color="orange lighten-2"
                  text
                  :to="'/registro/' + e.id.toString()"
                >
                  Datos del curso
                </v-btn>
              </div>
            </v-card-actions>
          </v-card>
            <br>
        </v-flex>
      </v-layout>
    </v-flex>
  </v-container>
</template>

<script>
export default {
  props: ["cursos", "titulo"],
  data: () => ({
    selectedItem: 1,
    link: "",
  }),
  methods: {},
};
</script>