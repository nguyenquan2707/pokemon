<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="handleBeforeStart($event)"
  />
  <interac-screen v-if="statusMatch === 'match'" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteracScreen from "./components/InteracScreen.vue";
export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      setting: {
        totalOfBlock: 0,
      },
    };
  },
  components: {
    MainScreen,
    InteracScreen,
  },
  methods: {
    handleBeforeStart(event) {
      console.log(event);
      this.setting.totalOfBlock = event.totalOfBlock;
      const firstCards = Array.from(
        { length: this.setting.totalOfBlock / 2 },
        (_, i) => i + 1
      );

      console.log(`firstCards=`, firstCards);

      this.statusMatch = "match";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
