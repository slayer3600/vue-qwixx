<template>
  <div>
    <v-card
      style="min-width:62px;"
      class="pa-3 rounded-lg text-center"
      :class="{ grey: this.state.disabled }"
      @click="toggleSelected"
      tile
    >
      <span class="text-h5 red--text font-weight-black" :class="textColor">
        {{ state.value }}
        <v-icon
          large
          v-if="this.state.selected"
          class="ml-n10 mt-n1 float-right"
          color="green darken-2"
          style="z-index: 9999"
        >
          mdi-check-bold
        </v-icon>
        <v-icon
          large
          v-if="this.state.value == 'L'"
          class="ml-n10 mt-n1 float-right"
          :class="textColor"
        >
          mdi-lock-open
        </v-icon>
      </span>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "QwixxButton",

  data: () => ({
    test: 55
  }),

  props: {
    color: String,
    state: Object
  },

  computed: {
    textColor() {
      return `${this.color}--text`;
    }
  },

  methods: {
    toggleSelected() {
      // console.log(`${this.color} - ${this.value} selected`);
      this.state.selected = !this.state.selected;
      this.$emit("numberClicked", this.state);
    }
  },

  created() {
    this.state.color = this.color;
  }
};
</script>

<style scoped>
.isSelected {
  color: gray;
}
</style>
