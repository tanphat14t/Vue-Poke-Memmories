<template>
  <div class="card" :class="{ disable: isDisable }">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlip }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackfaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object],
    },
    imgBackfaceUrl: {
      type: String,
      required: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isDisable: false,
      isFlip: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisable) return false;
      this.isFlip = !this.isFlip;
      if (this.isFlip) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFlip = false;
    },
    onEnableDisableMode() {
      this.isDisable = true;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  display: inline-block;
  perspective: revert-layer;
}
.card__inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card__inner.is-flipped {
  transform: rotateY(-198deg);
}
.card.disable .card__inner {
  cursor: default;
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 0.5rem;
  box-shadow: 0 2px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background-image: url("../assets/images/icon_back.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  width: 100%;
  height: 100%;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  width: 100%;
  height: 100%;
}
</style>
