<template>
  <v-app>  

    <HomeNavbar />
    <v-main>
      <v-container>
        <Nuxt :user.sync="user"/>
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} USACH</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      user : {},
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
