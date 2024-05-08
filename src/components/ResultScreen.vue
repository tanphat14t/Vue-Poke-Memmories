<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <p>{{ Math.round(timer / 1000) }} Second</p>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      require: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
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
p {
  font-size: 32px;
  line-height: normal;
  margin-bottom: 16px;
}

button {
  width: 120px;
  height: 52px;
  border: 1px solid var(--light);
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-family: var(--font);
  font-size: 20px;
  transition: all 0.4s;
}
button:hover {
  background: transparent;
  color: var(--light);
}
</style>
