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
        <QwixxRow
          color="red"
          :isReversed="false"
          @onScoreChange="onScoreChange"
        />
        <QwixxRow
          color="yellow"
          :isReversed="false"
          @onScoreChange="onScoreChange"
        />
        <QwixxRow
          color="green"
          :isReversed="true"
          @onScoreChange="onScoreChange"
        />
        <QwixxRow
          color="blue"
          :isReversed="true"
          @onScoreChange="onScoreChange"
        />

        <!-- Penalties -->
        <v-card
          class="d-flex flex-row pa-4 mb-2 justify-end d-inline"
          flat
          tile
        >
          <v-icon large>
            mdi-dice-5
          </v-icon>
          <v-icon x-large class="red--text">
            mdi-alpha-x
          </v-icon>
          <div class="mt-2 text-h5 font-weight-black">penalties</div>
          <div v-for="item in penalties" :key="item.index">
            <v-card
              outlined
              style="min-width:50px; min-height:50px;"
              class="pa-1 ml-3 rounded-lg"
              @click="onPenaltySelected(item)"
            >
              <v-icon x-large class="red" v-if="item.selected">
                mdi-alpha-x
              </v-icon>
            </v-card>
          </div>
        </v-card>

        <!-- Totals -->
        <v-card
          class="d-flex flex-row pa-4 mb-2 justify-space-around d-inline grey lighten-2"
          flat
          tile
        >
          <div class="mt-2 text-h5 font-weight-black">totals</div>
          <v-card
            style="min-width:80px;"
            class="pa-3 rounded-lg text-center text-h5 red lighten-4 font-weight-black"
          >
            {{ redScore }}
          </v-card>
          <div class="mt-2 text-h5 font-weight-black">+</div>
          <v-card
            style="min-width:80px;"
            class="pa-3 rounded-lg text-center text-h5 yellow lighten-4 font-weight-black"
          >
            {{ yellowScore }}
          </v-card>
          <div class="mt-2 text-h5 font-weight-black">+</div>
          <v-card
            style="min-width:80px;"
            class="pa-3 rounded-lg text-center text-h5 green lighten-4 font-weight-black"
          >
            {{ greenScore }}
          </v-card>
          <div class="mt-2 text-h5 font-weight-black">+</div>
          <v-card
            style="min-width:80px;"
            class="pa-3 rounded-lg text-center text-h5 blue lighten-4 font-weight-black"
          >
            {{ blueScore }}
          </v-card>
          <div class="mt-2 text-h5 font-weight-black">-</div>
          <v-card
            style="min-width:80px;"
            class="pa-3 rounded-lg text-center text-h5 font-weight-black"
          >
            {{ penaltyScore }}
          </v-card>
          <div class="mt-2 text-h5 font-weight-black">=</div>
          <v-card
            style="min-width:160px;"
            class="pa-3 rounded-lg text-center text-h5 font-weight-black"
          >
            {{ totalScore }}
          </v-card>
        </v-card>
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
    redScore: 0,
    yellowScore: 0,
    greenScore: 0,
    blueScore: 0,
    penaltyScore: 0,
    penalties: [
      { index: 1, selected: false },
      { index: 2, selected: false },
      { index: 3, selected: false },
      { index: 4, selected: false }
    ]
  }),

  methods: {
    onScoreChange(score, color) {
      // this.redScore = score;
      console.log(`Color score changed: ${color}`);
      switch (color) {
        case "red":
          this.redScore = score;
          break;
        case "yellow":
          this.yellowScore = score;
          break;
        case "green":
          this.greenScore = score;
          break;
        case "blue":
          this.blueScore = score;
          break;
      }
    },
    onPenaltySelected(item) {
      item.selected = !item.selected;
      this.penaltyScore = this.penaltyCalc;
    }
  },

  computed: {
    totalScore() {
      let totalScore =
        this.redScore +
        this.yellowScore +
        this.greenScore +
        this.blueScore -
        this.penaltyScore;
      return totalScore;
    },

    penaltyCalc() {
      let penalties = this.penalties.filter(item => item.selected == true);
      return penalties.length * 5;
    }
  }
};
</script>
