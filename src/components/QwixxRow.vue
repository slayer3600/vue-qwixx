<template>
  <v-card
    class="d-flex flex-row pa-4 mb-2 justify-space-between d-inline"
    flat
    tile
    :class="color"
  >
    <div v-for="item in qwixxNumbersList" :key="item.index">
      <QwixxButton :state="item" :color="color" @numberClicked="onNumberClicked" />
    </div>
  </v-card>
</template>

<script>
import QwixxButton from "@/components/QwixxButton";

export default {
  name: "QwixxRow",
  components: {
    // HelloWorld
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
    qwixxLock: { index: 12, value: "L", selected: false, disabled: false },
    qwixxLockReversed: { index: 0, value: "L", selected: false, disabled: false }
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
    }
  },

  methods: {
    onNumberClicked(selectedItem) {
      // console.log(`${JSON.stringify(this.qwixxNumbers)} emitted to parent.`);
      console.log(`${this.isReversed} isReversed to parent.`);
      console.log(`${JSON.stringify(selectedItem)} state to parent.`);
      this.qwixxNumbers.forEach(function(item) {
        if (this.isReversed) {
          if (item.index > selectedItem.index) {
            item.selected ? (item.disabled = false) : (item.disabled = true);
            console.log("I am more than selected value");
          }
        } else {
          if (item.index < selectedItem.index) {
            item.selected ? (item.disabled = false) : (item.disabled = true);
            console.log("I am less than selected value");
          }
        }
      }, this);
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
