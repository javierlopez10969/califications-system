<template>
  <v-card class="mx-auto" tile text-center>
    <v-list flat>
      <v-subheader>CURSOS </v-subheader>
      <v-list-item-group v-model="selectedItem" color="primary">
        <v-list-item v-for="(item, i) in cursos" :key="i" :to="'/cursos/'+item.id.toString()">
          <v-list-item-title
            v-text="item.name"
          ></v-list-item-title>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    selectedItem: 1,
    link: '',
  }),
  props: ["cursos"],
  methods: {
  },
};
</script>