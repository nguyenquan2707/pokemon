<template>
  <h1>Interact component..</h1>
  <card-flip
    v-for="(card, index) in cardsContext"
    :key="index"
    :urmBackImage="`images/${card}.png`"
    :card="card"
    @onFlip="rulesCheck($event)"
  />
</template>

<script>
import CardFlip from "./Card.vue";

export default {
  data() {
    return {
      rules: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: () => [],
    },
  },
  components: {
    CardFlip,
  },
  methods: {
    //Gía trị nhận card này là từ bên Card model gửi ra.
    rulesCheck(card) {
      console.log(card);
      //match, Từ rules arrays
      if (this.rules.length === 2) return false;
      //not match
    },
  },
};
</script>
