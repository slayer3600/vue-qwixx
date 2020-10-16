<template>
  <v-card
    class="d-flex flex-row pa-4 mb-2 justify-space-between d-inline"
    flat
    tile
    :class="color"
  >
    <div v-for="item in qwixxNumbersList" :key="item.index">
      <QwixxButton
        :state="item"
        :color="color"
        @numberClicked="onNumberClicked"
      />
    </div>
  </v-card>
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
      { index: 1, value: "2", selected: false, disabled: false },
      { index: 2, value: "3", selected: false, disabled: false },
      { index: 3, value: "4", selected: false, disabled: false },
      { index: 4, value: "5", selected: false, disabled: false },
      { index: 5, value: "6", selected: false, disabled: false },
      { index: 6, value: "7", selected: false, disabled: false },
      { index: 7, value: "8", selected: false, disabled: false },
      { index: 8, value: "9", selected: false, disabled: false },
      { index: 9, value: "10", selected: false, disabled: false },
      { index: 10, value: "11", selected: false, disabled: false },
      { index: 11, value: "12", selected: false, disabled: false }
    ],
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
    ],
    qwixxLock: { index: 12, value: "L", selected: false, disabled: false },
    qwixxLockReversed: {
      index: 0,
      value: "L",
      selected: false,
      disabled: false
    }
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
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.qwixxNumbers.push(this.qwixxLockReversed);
        return this.qwixxNumbers;
      } else {
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.qwixxNumbers.push(this.qwixxLock);
        return this.qwixxNumbers;
      }
    },

    qwixxItemsSelected() {
      var count = this.qwixxNumbers.filter(item => item.selected == true);
      return count.length;
    },

    score() {
      var multiplier = this.qwixxScoreMultipliers.filter(
        item => item.count == this.qwixxItemsSelected
      );
      var score = multiplier[0].score;
      this.$emit("onScoreChange", score, this.color);
      return score;
    }
  },

  methods: {
    onNumberClicked(selectedItem) {
      // console.log(`${JSON.stringify(this.qwixxNumbers)} emitted to parent.`);
      // console.log(`${this.isReversed} isReversed to parent.`);
      console.log(`${JSON.stringify(selectedItem)} state to parent.`);

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

      console.log(`Score: ${this.score}`);
      // this.qwixxNumbers.some(function(item) {
      //   if (this.isReversed) {
      //     if (item.index > selectedItem.index) {
      //       if (selectedItem.selected) {
      //         console.log("I was selected.");
      //         item.selected ? (item.disabled = false) : (item.disabled = true);
      //       } else {
      //         console.log("I was de-selected.");
      //         // item.selected ? (item.disabled = false) : (item.disabled = false);
      //         if (item.selected) {
      //           return true;
      //         } else {
      //           item.disabled = false;
      //         }
      //       }
      //     }
      //   } else {
      //     if (item.index < selectedItem.index) {
      //       item.selected ? (item.disabled = false) : (item.disabled = true);
      //       console.log("I am less than selected value");
      //     }
      //   }
      // }, this);
    }

    // updateBoard(selectedItem, updatedItem) {
    //   if (this.isReversed) {
    //     if (updatedItem.index > selectedItem.index) {
    //       updatedItem.disabled = true;
    //       console.log("I am more than selected value");
    //     }
    //   } else {
    //     if (updatedItem.index < selectedItem.index) {
    //       updatedItem.disabled = true;
    //       console.log("I am less than selected value");
    //     }
    //   }
    // }
  }
};
</script>

<style></style>
