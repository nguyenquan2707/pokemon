<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="handleBeforeStart($event)"
  />
  <!--Khi bấm vào chọn level, sẽ gửi ra event onStart kèm theo sự kiện -->
  <!-- Từ sự kiện sẽ truyền vào hàm handleBeforeStart để tính cardsContext -->
  <!-- Đem cardsContext này vào model interac-screen -->
  <!-- Giá trị cardsContext là {0: 4, 1: 2, 2: 4, 3: 1, 4: 6, 5: 3, 6: 3, 7: 8, 8: 2, 9: 5, 10: 6, 11: 1, 12: 5, 13: 8, 14: 7, 15: 7} -->
  <!-- Trong model InteracScreen loop ra tạo card tương ứng -->
  <!-- Trong model InteracScreen loop ra tạo urmBackImage để tạo hình cho card-->
  <!--  Trong model InteracScreen gửi data card xuống cho Card model bằng dòng code ':card="card"' -->
  <!-- Khi bấm vào card, sẽ gửi sự kiện onFlip kèm theo data là card phía trên gửi ngược ra cho InteracScreen và gửi vào hàm rulesCheck -->
  <!-- Từ hàm rulesCheck sẽ xử lý logic cho game. -->
  <interac-screen
    v-if="statusMatch === 'match'"
    :cardsContext="setting.cardsContext"
  />
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
