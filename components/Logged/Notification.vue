<template>
  <div>
    <v-menu offset-y>
      <template #activator="{ on: onMenu }">
        <v-tooltip bottom>
          <template #activator="{ on: onTooltip }">
            <v-btn v-on="{ ...onMenu, ...onTooltip }" icon>
              <v-badge
                :content="notifications.length"
                :value="notifications.length"
                color="green"
                overlap
              >
                <v-icon large> mdi-bell </v-icon>
              </v-badge>
            </v-btn>
          </template>

          <span>Notificaciones</span>
        </v-tooltip>
      </template>

      <LoggedNotificationList />
    </v-menu>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: "New mail from Adam Joe" },
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me 2" },
      ],
      messages: 0,
      show: false,
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
<style>
/* This is for documentation purposes and will not be needed in your application */
#create .v-speed-dial {
  position: absolute;
}
</style>