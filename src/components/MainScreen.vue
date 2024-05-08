<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button class="button" @click="onStart(16)">
        <span class="number">4x4</span>
        <span class="text">Easy</span>
      </button>
      <button class="button" @click="onStart(36)">
        <span class="number">6x6</span>
        <span class="text">Normal</span>
      </button>
      <button class="button" @click="onStart(64)">
        <span class="number">8x8</span>
        <span class="text">Hard</span>
      </button>
      <button class="button" @click="onStart(100)">
        <span class="number">10x10</span>
        <span class="text">Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalofBlocks) {
      this.$emit("onStart", { totalofBlocks });
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--dark);
  width: 100%;
  height: 100vh;
  color: var(--light);
}
h1 {
  font-size: 72px;
  line-height: normal;
  margin-bottom: 12px;
}
h3 {
  font-size: 32px;
  line-height: normal;
  margin-bottom: 16px;
}
.actions {
  display: flex;
  gap: 2rem;
  flex-wrap: nowrap;
  max-width: 1170px;
  width: 100%;
  margin: 0 auto;
}
button {
  width: calc(100% / 4 - 2rem);
  border: 1px solid var(--light);
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  aspect-ratio: 1;
  cursor: pointer;
}
button span.number {
  font-family: var(--font);
  font-size: 32px;
  line-height: normal;
  margin-bottom: 8px;
}
button span.text {
  font-family: var(--font);
  font-size: 20px;
  line-height: normal;
}
</style>
