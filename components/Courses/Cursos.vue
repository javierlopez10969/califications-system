<template>
  <v-container>
    <p class="text-h4 text--primary mb-0 text-left">{{ titulo }}</p>
    <v-flex d-flex>
      <v-layout wrap>
        <v-flex md6 v-for="(item, i) in cursos" :key="i">
          <v-card
            class="mt-8 text-left"
            max-width="470"
          >
            <v-img
              src="https://uvirtual.usach.cl/moodle/theme/image.php/eguru/theme/1640116840/cs02/no-image"
              height="150px"
            ></v-img>
            <v-card-title>
              {{ item.name }}
            </v-card-title>
            <v-card-actions>
              <!--V -if si tiene roles para editar este curso-->
              <div v-if="item.activate === true">
                <v-btn
                  color="orange lighten-2"
                  text
                  :to="'/cursos/' + item.id.toString()"
                >
                  Datos del curso
                </v-btn>
              </div>
              <div v-else>
                <v-btn
                  color="orange lighten-2"
                  text
                  :to="'/registro/' + item.id.toString()"
                >
                  Datos del curso
                </v-btn>
              </div>
            </v-card-actions>
          </v-card>
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