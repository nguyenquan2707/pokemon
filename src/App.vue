<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="handleBeforeStart($event)"
  />
  <interac-screen v-if="statusMatch === 'match'" :cardsContext="cardsContext" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteracScreen from "./components/InteracScreen.vue";
import { shuffled } from "./utils/arrays";
export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      setting: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
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

      let secondCards = [...firstCards];
      let cards = [...firstCards, ...secondCards];
      this.setting.cardsContext = shuffled(cards);
      this.setting.startedAt = new Date().getTime;

      console.log(`cardsContext=`, this.setting.cardsContext);

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
