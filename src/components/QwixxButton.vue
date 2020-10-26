<template>
  <div>
    <v-card
      style="min-width:62px;"
      class="pa-3 text-center"
      :class="{
        grey: this.state.disabled,
        'rounded-lg': this.state.value < 13,
        'rounded-circle': this.state.value == 'L'
      }"
      :disabled="this.state.disabled"
      @click="toggleSelected"
      tile
    >
      <span class="text-h5 font-weight-black" :class="textColor">
        <span v-if="this.state.value < 13">
          {{ state.value }}
        </span>
        <span v-else>
          &zwnj;
        </span>
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
          class="ml-n10 mt-n1 float-right mdi-rotate-45"
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
    //
  }),

  props: {
    index: Number,
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
      this.state.selected = !this.state.selected;
      this.$emit("numberClicked", this.state, this.index);
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
