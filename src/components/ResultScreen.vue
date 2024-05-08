<template>
  <div class="screen">
    <h1>Congratulation</h1>
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
<style lang="css" scoped></style>
