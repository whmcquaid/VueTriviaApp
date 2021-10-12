<template>
  <div class="menus">
    <form autofocus="true" @submit.prevent="changeEndpoint">
      <div class="numSelect">
        <label for="questionNum">How many trivia questions?</label>
        <select
          v-model="numOfQuestions"
          required="true"
          name="Number of Questions"
          id="questionNum"
          style="width: 60px"
        >
          <option disabled value=""
            >--Please choose number of questions--</option
          >
          <option value="5">5</option>
          <option value="10">10</option>
          <option value="15">15</option>
          <option value="20">20</option>
          <option value="25">25</option>
          <option value="30">30</option>
        </select>
      </div>
      <div class="categorySelect">
        <label for="category">Pick a category.</label>
        <select
          v-model="category"
          required="true"
          name="Trivia Category"
          id="category"
          tyle="width: 130px"
        >
          <option disabled value="">--Please choose a category--</option>
          <option value="9">General Knowledge</option>
          <!-- <option value="20">Mythology</option> -->
          <option value="23">History</option>
          <option value="11">Movies</option>
          <option value="12">Music</option>
          <option value="14">TV</option>
          <option value="15">Video Games</option>
          <option value="18">Computers</option>
          <option value="21">Sports</option>
          <!-- // <option value="27">Animals</option> -->
          <!-- <option value="28">Vehicles</option> -->
        </select>
      </div>
      <div class="diffSelect">
        <label for="difficulty">Set the difficulty.</label>
        <select
          v-model="difficulty"
          required="true"
          name="Trivia Difficulty"
          id="difficulty"
          tyle="width: 70px"
        >
          <option disabled value=""
            >--Please choose number of questions--</option
          >
          <option value="easy">Smart</option>
          <option value="medium">Really Smart</option>
          <option value="hard">Genius</option>
        </select>
      </div>
      <div class="submitButton-container">
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      numOfQuestions: '',
      category: '',
      difficulty: '',
    };
  },

  computed: {
    endpointString() {
      const numOfQuestions = this.numOfQuestions || '10';
      const category = this.category || '15';
      const difficulty = this.difficulty || 'easy';
      return `https://opentdb.com/api.php?amount=${numOfQuestions}&category=${category}&difficulty=${difficulty}&type=multiple`;
    },
  },
  methods: {
    changeEndpoint() {
      let newEndpoint = this.endpointString;
      this.$emit('endpoint', newEndpoint);
    },
  },
};
</script>
<style scoped>
.menus {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-self: center;
  text-align: right;
  max-width: 95vw;
}
select {
  margin: 5px;
}
</style>
