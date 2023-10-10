<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="card" :class="{ disabled: isDisabled }">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('../assets/images/' + imageUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imageUrl: {
      type: String,
      required: true,
    },
    cardValue: {
      // String, Number, Object...
      type: [Array, String, Number, Object],
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false;

      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("openCard", this.cardValue);
      }
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnabledDisableMode() {
      this.isDisabled = true;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-top: 1rem;
  width: 90px;
  height: 120px;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card.disabled .card__inner {
  cursor: default;
}

.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center;
  height: 100%;
  width: 100%;
  background-size: 40px 40px;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--back .card__content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
}
</style>
