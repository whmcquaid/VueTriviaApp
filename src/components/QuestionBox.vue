<template>
  <div class="question-box">
    <div class="question">
      <h3 v-html="currentQuestion.question" />
    </div>
    <div
      class="selection"
      v-for="(answer, index) in shuffledAnswers"
      :key="index"
      @click="selectAnswer(index)"
      :class="[
        !hasBeenSubmitted && selectedIndex === index
          ? 'selected'
          : hasBeenSubmitted && correctIndex === index
          ? 'correct'
          : hasBeenSubmitted && correctIndex !== index
          ? 'incorrect'
          : '',
      ]"
    >
      <p v-html="answer"></p>
    </div>

    <button
      class="submit"
      @click="submitAnswer"
      :disabled="hasBeenSubmitted || selectedIndex === null"
    >
      Submit
    </button>
    <button class="next" @click="next">Next</button>
  </div>
</template>

<script>
export default {
  props: {
    currentQuestion: {
      type: Object,
      default: function() {
        return {};
      },
    },
    next: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: [],
      correctIndex: null,
      hasBeenSubmitted: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
  watch: {
    currentQuestion: {
      // immediate: true,
      handler() {
        this.hasBeenSubmitted = false;
        this.selectedIndex = null;
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffle(array) {
      let curId = array.length;
      // There remain elements to shuffle
      while (0 !== curId) {
        // Pick a remaining element
        let randId = Math.floor(Math.random() * curId);
        curId -= 1;
        // Swap it with the current element.
        let tmp = array[curId];
        array[curId] = array[randId];
        array[randId] = tmp;
      }
      return array;
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.shuffledAnswers = this.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
      this.hasBeenSubmitted = true;
    },
  },
};
</script>

<style scoped>
.question-box {
  background-color: rgba(138, 135, 135, 0.8);
  text-align: center;
}
.submit {
  background-color: rgba(167, 156, 209, 0.842);
  margin: 10px;
}
.next {
  background-color: rgb(40, 180, 115, 0.6);
}
.selection {
  background-color: rgba(167, 236, 236, 0.8);
  border: 2px solid black;
}
.selection:hover {
  background-color: rgba(86, 233, 233, 0.5);
  cursor: pointer;
}
.selected {
  background-color: rgba(199, 207, 207, 0.9);
}
.correct {
  background-color: springgreen;
}
.incorrect {
  background-color: tomato;
}
</style>
