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
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  align-content: center;
  background-color: rgb(233, 243, 174);
}
.header {
  align-self: center;
  background-color: rgb(32, 235, 14);
  text-align: center;
  border-radius: 20px;
  width: 60%;
}
</style>
