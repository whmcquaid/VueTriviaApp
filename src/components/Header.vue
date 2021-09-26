<template>
  <div class="header">
    <h1>Vue trivia app</h1>
    <h3>{{ this.totalCorrect }}/{{ this.totalQuestions }}</h3>
  </div>
</template>
<script>
export default {
  props: {
    totalQuestions: Number,
    totalCorrect: Number,
  },
};
</script>

<style scoped>
.container {
  max-width: 70vw;
  align-content: center;
}
.header {
  text-align: center;
  background-color: rgba(167, 236, 236, 0.8);
}
</style>
