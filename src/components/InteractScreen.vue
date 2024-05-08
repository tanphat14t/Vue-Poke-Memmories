<template>
  <div class="screen">
    <h1>interact screen</h1>
    <div
      class="screen__inner"
      :style="{
        'grid-template-columns': `repeat(${Math.sqrt(
          cardsContext.length
        )}, auto)`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackfaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>
<script>
import CardFlip from "./CardItem.vue";
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
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("right....");
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
        this.rules = [];

        const disableElement = document.querySelectorAll(
          ".screen .card.disable"
        );
        if (
          disableElement &&
          disableElement.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          //close two card
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // reset rules to []
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  text-align: center;
  padding-top: 20px;
}
.screen__inner {
  width: 60%;
  display: grid;
  grid-template-columns: repeat(4, auto);
  margin: 2rem auto;
  height: 80%;
  gap: 8px;
}
@media (max-width: 991px) {
  .screen__inner {
    width: 100%;
  }
}
@media (max-width: 525px) {
  .screen__inner {
    height: 90%;
  }
}
</style>
