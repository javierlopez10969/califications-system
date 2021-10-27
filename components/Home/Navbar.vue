<template>
  <v-app-bar
    dense
    color="white"
    elevate-on-scroll
    scroll-target="#scrolling-techniques-7"
  >
    <NuxtLink to="/">
      <v-toolbar-title>Sistema de Notas</v-toolbar-title>
    </NuxtLink>

    <v-spacer></v-spacer>
    <NuxtLink to="/login">
      <v-btn rounded color="primary" dark> Iniciar Sesión </v-btn>
    </NuxtLink>
  </v-app-bar>
</template>