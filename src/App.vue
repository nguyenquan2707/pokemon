<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interac-screen
    v-if="statusMatch === 'match'"
    :cardsContext="this.settings.cardsContext"
    @onFinish="onGetResult()"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="this.timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <copy-right />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteracScreen from "./components/InteracScreen.vue";
import ResultScreen from "./components/Result.vue";
import { shuffled } from "./utils/arrays";
import CopyRight from "./components/CopyRight.vue";
export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      timer: 0,
    };
  },
  components: {
    MainScreen,
    InteracScreen,
    ResultScreen,
    CopyRight,
  },
  methods: {
    onHandleBeforeStart(event) {
      this.settings.totalOfBlocks = event.totalOfBlocks;
      let firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (__, i) => i + 1
      );
      let secondCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (__, i) => i + 1
      );

      let cards = [...firstCards, ...secondCards];

      this.settings.cardsContext = shuffled(cards);

      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
    onGetResult() {
      //go to result component.
      this.statusMatch = "result";
      //get time
      this.timer = new Date().getTime() - this.settings.startedAt;
    },
  },
};
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
