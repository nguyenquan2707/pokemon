<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="card">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      v-on:click="onToggleFlipCard()"
    >
      <div class="card__face card__face--front">
        <div class="card-content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card-content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + urmBackImage)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    urmBackImage: {
      type: String,
      require: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
  },
  data() {
    return {
      isFlipped: false,
    };
  },
  methods: {
    //Khi click vào card, thì card sẽ gửi ra ngoài 1 sự kiện, kèm theo giá trị card, card này define ở props.
    onToggleFlipCard() {
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onFlip", this.card);
      }
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}

/* Đóng vai trò cố định vị trí khi quay */
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card__face {
  /* Trước sau như 1 */
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
}
.card__face--front .card-content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40%;
  height: 100%;
  width: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card-content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
