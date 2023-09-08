<template>
  <div class="screen">
    <h1>POKE memories</h1>
    <h3>Select to start the game</h3>
    <div class="action">
      <button v-on:click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button v-on:click="onStart(32)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button v-on:click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button v-on:click="onStart(100)">
        <span>10X10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalOfBlock) {
      console.log("heere", totalOfBlock);
      this.$emit("onStart", { totalOfBlock });
    },
  },
};
</script>
