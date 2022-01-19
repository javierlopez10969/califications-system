<template>
  <v-carousel cycle height="400" hide-delimiter-background show-arrows-on-hover class="mt-6">
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      reverse-transition="fade-transition"
      transition="fade-transition"
    ></v-carousel-item>
  </v-carousel>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          src: "https://i.ibb.co/d76ySQ6/fing-v1-png-3648x1270-q85-subsampling-2.png",
        },
        {
          src: "https://pbs.twimg.com/media/EyjSw4pWgAU1bcj.jpg",
        },
        {
          src: "https://i.ibb.co/DVvkwWw/4fc3xy.png",
        },
        {
          src: "https://cdn.vuetifyjs.com/images/carousel/planet.jpg",
        },
      ],
    };
  },
};
</script>