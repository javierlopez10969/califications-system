<template>
  <div>
    
    <nuxt-child :curso="curso" />
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "",
      titleTemplate: `%s ${this.curso.name}`,
    };
  },
  async asyncData({ $axios, params }) {
    let response = await $axios.post('/courses/' + params.id +'/');
    console
    let curso = response.data.course;
    return {
      curso,
    };
  },
};
</script>
<style lang="scss" scoped>
</style>