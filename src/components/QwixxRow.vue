<template>
  <div>
    <v-card
      class="d-flex flex-row pa-4 mb-2 justify-space-between d-inline"
      flat
      tile
      :class="color"
    >
      <v-icon x-large color="grey darken-3" class="ml-n12 mdi-rotate-90">
        mdi-triangle
      </v-icon>
      <div v-for="(item, index) in qwixxNumbersList" :key="item.value">
        <QwixxButton
          :index="index"
          :state="item"
          :color="color"
          @numberClicked="onNumberClicked"
        />
      </div>
    </v-card>
  </div>
</template>

<script>
import QwixxButton from "@/components/QwixxButton";

export default {
  name: "QwixxRow",
  components: {
    QwixxButton
  },

  data: () => ({
    numbers: 12,
    qwixxNumbers: [
      { value: "2", selected: false, disabled: false },
      { value: "3", selected: false, disabled: false },
      { value: "4", selected: false, disabled: false },
      { value: "5", selected: false, disabled: false },
      { value: "6", selected: false, disabled: false },
      { value: "7", selected: false, disabled: false },
      { value: "8", selected: false, disabled: false },
      { value: "9", selected: false, disabled: false },
      { value: "10", selected: false, disabled: false },
      { value: "11", selected: false, disabled: false },
      { value: "12", selected: false, disabled: false }
    ],
    qwixxLock: { value: "L", selected: false, disabled: false },
    qwixxScoreMultipliers: [
      { count: 1, score: 1 },
      { count: 2, score: 3 },
      { count: 3, score: 6 },
      { count: 4, score: 10 },
      { count: 5, score: 15 },
      { count: 6, score: 21 },
      { count: 7, score: 28 },
      { count: 8, score: 26 },
      { count: 9, score: 45 },
      { count: 10, score: 55 },
      { count: 11, score: 66 },
      { count: 12, score: 78 }
    ]
  }),

  props: {
    color: String,
    isReversed: Boolean
  },

  computed: {
    qwixxNumbersList() {
      if (this.isReversed) {
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.qwixxNumbers = this.qwixxNumbers.slice(0).reverse();
      }
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.qwixxNumbers.push(this.qwixxLock);
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.qwixxNumbers[10].disabled = true;
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.qwixxNumbers[11].disabled = true;
      return this.qwixxNumbers;
    },

    qwixxItemsSelected() {
      var count = this.qwixxNumbers.filter(item => item.selected == true);
      return count.length;
    },

    score() {
      var multiplier = this.qwixxScoreMultipliers.filter(
        item => item.count == this.qwixxItemsSelected
      );
      var score = multiplier[0] === undefined ? 0 : multiplier[0].score;
      console.log(`Computed Score: ${score}`);
      this.$emit("onScoreChange", score, this.color);
      return score;
    },

    getHighestSelectedIndex() {
      let highestSelectedIndex = 0;
      for (let index = 0; index < this.qwixxNumbers.length; index++) {
        // const element = array[index];
        if (this.qwixxNumbers[index].selected === true) {
          highestSelectedIndex = index;
        }
      }
      return highestSelectedIndex;
    }
  },

  methods: {
    onNumberClicked(selectedItem, index) {
      console.log(`Index: ${index}`);
      console.log(`Selected: ${selectedItem.selected}`);
      //enable/disable last item
      if (this.qwixxItemsSelected >= 5) {
        this.qwixxNumbers[10].disabled = false;
        this.qwixxNumbers[11].disabled = false;
      } else {
        this.qwixxNumbers[10].disabled = true;
        this.qwixxNumbers[11].disabled = true;
      }

      if (
        this.isReversed &&
        (selectedItem.value == "L" || selectedItem.value == "2")
      ) {
        console.log("You selected L or 2");
        if (this.qwixxItemsSelected <= 5) {
          console.log("You must select at least 5");
          selectedItem.selected = false;
        }
      } else if (
        !this.isReversed &&
        (selectedItem.value == "L" || selectedItem.value == "12")
      ) {
        console.log("You selected L or 12");
        if (this.qwixxItemsSelected <= 5) {
          console.log("You must select at least 5");
          selectedItem.selected = false;
        }
      }

      console.log(`Highest Selected: ${this.getHighestSelectedIndex}`);
      this.toggleDisable(index);
      console.log(`Score: ${this.score}`);
    },

    toggleDisable(selectedIndex) {
      let highestIndex = 0;
      highestIndex =
        this.getHighestSelectedIndex > selectedIndex
          ? this.getHighestSelectedIndex
          : selectedIndex;
      for (let index = 0; index <= highestIndex; index++) {
        if (this.qwixxNumbers[index].selected === false) {
          this.qwixxNumbers[index].disabled = true;
        } else {
          this.qwixxNumbers[index].disabled = false;
        }

        if (index >= this.getHighestSelectedIndex) {
          this.qwixxNumbers[index].disabled = false;
        }
      }
    }
  }
};
</script>

<style></style>
