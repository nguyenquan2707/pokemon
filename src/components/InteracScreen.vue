<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imageUrl="`${card}.png`"
      :cardValue="{ index, cardData: card }"
      @openCard="checkRule($event)"
    />
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
      } else if (
        this.rule.length === 2 &&
        this.rule[0].cardData !== this.rule[1].cardData
      ) {
        console.log(`wrong case =`, cardValue);
        setTimeout(() => {
          // this.$refs[`card-${this.rule[0].index}`].onFlipBackCard();
          // this.$refs[`card-${this.rule[1].index}`].onFlipBackCard();
          this.rule = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>
