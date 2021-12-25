<template>
  <div>
    <ul v-for="mountain in mountains" :key="mountain.id">
      <NuxtLink :to="'admin/'+`${mountain.continent.toLowerCase()}/${mountain.slug}`">
        <li>{{ mountain.title }}</li>
      </NuxtLink>
    </ul>
  </div>
</template>
<script>
export default {
  layout: "logged",
  async asyncData() {
    const mountains = await fetch("https://api.nuxtjs.dev/mountains").then(
      (res) => res.json()
    );

    return { mountains };
  },
};
</script>
