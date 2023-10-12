<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="screen">
    <h1>Congratulation</h1>
    <p>{{ timer / 1000 }} seconds</p>
    <button @click="onStartAgain()">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      require: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
