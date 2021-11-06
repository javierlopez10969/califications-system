<template>
  <div>
    <v-app-bar dense>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>Sistema de notas</v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-bell</v-icon>
      </v-btn>
      <v-btn href="/login" rounded color="red"> Cerrar sesión</v-btn>
      <v-menu left bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </div>
</template>
<script>
export default {
  data() {
    return {
      notifications: [
        {
          title: "New mail from Adam Joe",
          color: "light-blue",
          icon: "email",
          actionAt: "12 min ago",
          isActive: true,
          onClick: () => {
            const vm = this;

            vm.$router.push({ name: "Mailbox" });
          },
        },
        {
          title: "Scheculed meeting",
          color: "red",
          icon: "calendar_today",
          actionAt: "46 min ago",
          isActive: true,
          onClick: () => {
            const vm = this;

            vm.$router.push({ name: "Calendar" });
          },
        },
        {
          title: "New mail from Github",
          color: "light-blue",
          icon: "email",
          isActive: true,
          timeLabel: "2 hour ago",
          onClick: () => {
            const vm = this;

            vm.$router.push({ name: "Mailbox" });
          },
        },
      ],
    };
  },
};
</script>
