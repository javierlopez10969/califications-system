<template>
  <div>
    We are in title: {{ video.title }}.
    <nuxt-link :to="`/videos/${video.id}/edit`">
      <button>Edit</button>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  props: ["video"],
  head: {
    title: "Video",
  },
};
</script>

<style lang="scss" scoped>
</style> 