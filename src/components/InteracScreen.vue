<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imageUrl="`${card}.png`"
      :cardValue="card"
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
      if (this.rule.length === 2 && this.rule[0] === this.rule[1]) {
        console.log(`right case =`, cardValue);
      } else if (this.rule.length === 2 && this.rule[0] !== this.rule[1]) {
        console.log(`wrong case =`, cardValue);
        this.rule = [];
      } else {
        return false;
      }
    },
  },
};
</script>
