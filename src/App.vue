<template>
  <div class="container">
    <Header :totalCorrect="totalCorrect" :totalQuestions="totalQuestions" />
    <QuestionBox
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
      :hasBeenSubmitted="hasBeenSubmitted"
    />
    <Menu @endpoint="updateEndpoint" />
  </div>
</template>

<script>
import MenuVue from './components/Menu.vue';
import HeaderVue from './components/Header.vue';
import QuestionBoxVue from './components/QuestionBox.vue';
export default {
  name: 'App',
  components: {
    Menu: MenuVue,
    Header: HeaderVue,
    QuestionBox: QuestionBoxVue,
  },
  data() {
    return {
      answers: [],
      questions: [],
      index: 0,
      totalCorrect: 0,
      totalQuestions: 0,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.totalCorrect++;
        this.totalQuestions++;
      } else {
        this.totalQuestions++;
      }
    },
    async updateEndpoint(newEndpoint) {
      await fetch(newEndpoint, {
        method: 'get',
      })
        .then((res) => res.json())
        .then((jsonData) => {
          this.questions = jsonData.results;
        });
    },
    hasBeenSubmitted() {},
  },

  mounted() {
    const defaultEndpoint =
      'https://opentdb.com/api.php?amount=10&type=multiple';
    this.updateEndpoint(defaultEndpoint);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #288ef5;
  margin-top: 60px;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: rgb(233, 243, 174);
  height: 100vh;
}
</style>
