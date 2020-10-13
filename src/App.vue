<template>
  <v-app>
    <!-- <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar> -->

    <v-main>
      <v-container>
        <h1>QWIXX</h1>
        <QwixxRow color="red" :isReversed="false" />
        <QwixxRow color="yellow" :isReversed="false" />
        <QwixxRow color="green" :isReversed="true" />
        <QwixxRow color="blue" :isReversed="true" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import QwixxRow from "@/components/QwixxRow";

export default {
  name: "App",

  components: {
    QwixxRow
  },

  data: () => ({
    //
  })
};
</script>
