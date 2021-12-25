<template>
    <v-container class="pa-5">
        <v-row class="mb-20">
            <v-col>
                <p class="text-h4 mb-1 text-left">Información del curso</p>
                <v-divider> </v-divider>
                <v-container class="pa-0">
                <v-list two-line class="pa-2">
                    <v-list-item-group two-line>
                        <v-list-item-content>
                            <v-list-item-title>
                                <p class="text-h6 font-weight-bold mb-0">Asignatura</p>
                            </v-list-item-title>
                            <v-list-item-subtitle>
                                <p class="text-h5">{{curso.name}}</p>
                            </v-list-item-subtitle>
                        </v-list-item-content>
                        <v-list-item-content>
                            <v-list-item-title>
                                <p class="text-h6 font-weight-bold mb-0">Descripción de la asignatura</p>
                            </v-list-item-title>
                            <v-list-item-subtitle v-if="curso.description != ''">
                                <p class="text-h5">{{curso.description}}</p>
                            </v-list-item-subtitle>
                            <v-list-item-subtitle v-else>Sin descripción.</v-list-item-subtitle>
                        </v-list-item-content>
                    </v-list-item-group>    
                </v-list>
                </v-container>
            </v-col>
            <v-col>
                <p class="text-h4 mb-1 text-left">Notas del curso</p>
                <v-divider> </v-divider>
                <v-container>
                    <h5>aquí van las notas del curso</h5>
                </v-container>
            </v-col>
        </v-row>
    </v-container>

</template>

<script>
export default {
  props : ["curso"],
    data: () => ({
      items: [
        { header: 'Today' },
        { avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg', title: 'Brunch this weekend?', subtitle: `<span class="font-weight-bold">Ali Connors</span> &mdash; I'll be in your neighborhood doing errands this weekend. Do you want to hang out?` },
        { divider: true, inset: true },
        { avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg', title: 'Summer BBQ <span class="grey--text text--lighten-1">4</span>', subtitle: `<span class="font-weight-bold">to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this weekend.` },
        { divider: true, inset: true },
        { avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg', title: 'Oui oui', subtitle: '<span class="font-weight-bold">Sandra Adams</span> &mdash; Do you have Paris recommendations? Have you ever been?' },
      ],
    }),
}
</script>