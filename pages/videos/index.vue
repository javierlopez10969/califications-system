<template>
  <div>
    <nuxt-child />
    <h1>Videos</h1>
    <div v-for="video in videos" :key="video.id">
      <nuxt-link :to="`/videos/${video.id}`">{{ video.title }}</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  head: {
    title: "Vue Screencasts - Video List",
  },
  async asyncData({ $axios }) {
    let response = await $axios.get(
      "https://jsonplaceholder.typicode.com/todos/"
    );
    let videos = response.data;
    return {
      videos,
    };
  },
};
</script>

<style lang="scss" scoped>
</style> 