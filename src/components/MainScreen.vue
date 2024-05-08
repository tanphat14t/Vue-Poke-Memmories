<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button class="button" @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button class="button" @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button class="button" @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button class="button" @click="onStart(100)">
        <span>10x10</span>
        <span>Super Hard</span>
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
<style lang="css"></style>
