<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imageUrl="`${card}.png`"
        :cardValue="{ index: index, cardData: card }"
        :cardsContext="cardsContext"
        @openCard="checkRule($event)"
      />
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rule: [],
    };
  },
  methods: {
    checkRule(cardValue) {
      if (this.rule.length === 2) {
        return false;
      }
      this.rule.push(cardValue);
      console.log(cardValue);
      if (
        this.rule.length === 2 &&
        this.rule[0].cardData === this.rule[1].cardData
      ) {
        console.log(`right case =`, cardValue);
        //add class disabled to card
        this.$refs[`card-${this.rule[0].index}`][0].onEnabledDisableMode();
        this.$refs[`card-${this.rule[1].index}`][0].onEnabledDisableMode();
        //reset rule to []
        this.rule = [];

        let openedElement = document.querySelectorAll(".screen .card.disabled");
        if (
          openedElement &&
          openedElement.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 2000);
        }
      } else if (
        this.rule.length === 2 &&
        this.rule[0].cardData !== this.rule[1].cardData
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rule[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rule[1].index}`][0].onFlipBackCard();
          this.rule = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
