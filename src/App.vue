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
    };
  },
  components: {
    MainScreen,
    InteracScreen,
  },
  methods: {
    handleBeforeStart(event) {
      console.log(event);
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
