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
    rulesCheck()
  },
};
</script>
