<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <!--  <copy-right-screen /> -->
</template>
<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";

import { shuffled } from "./utils/array";
// import CopyRightScreen from "./components/CopyRightScreen.vue";
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    // CopyRightScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log(config);
      this.settings.totalOfBlock = config.totalofBlocks;
      const firstCard = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const secondCard = [...firstCard];
      const Cards = [...firstCard, ...secondCard];

      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(Cards)))
      );

      this.settings.startedAt = new Date().getTime();
      // data ready
      this.statusMatch = "match";
    },

    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
      // switch screen
    },
  },
};
</script>
