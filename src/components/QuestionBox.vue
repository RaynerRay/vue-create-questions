<template>
  <div>
    <b-jumbotron>
      <template slot="lead">
        <p>{{ currentQuestion.description }}</p>
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers" 
          :key="index"
          @click="selectAnswer(index)"
          :class="[
          !answered && selectedIndex === index ? 'selected' : 
          answered && correctIndex === index ? 'correct' :
          answered && selectedIndex === index && correctIndex !==  index ? 'incorrect' : ''
          ]"
          >
          {{ answer.text }}
        </b-list-group-item>
  
      </b-list-group>

      

      <b-button variant="primary" @click="previous">Previous</b-button>
      <b-button variant="success" @click="next">Next</b-button>
      <b-button 
      variant="success" 
      @click="submitAnswer"
      :disabled="selectedIndex === null || answered"
      >
      Submit
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function,
    previous: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.alternatives];
      return answers;
    },
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },

    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;

      this.increment(isCorrect);
    },

    shuffleAnswers() {
      let answers = [...this.currentQuestion.alternatives];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.alternatives.isCorrect
      );
      console.log(this.correctIndex);
    },
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #e9ecef;
  cursor: pointer;
}
.selected {
  background-color: rgb(122, 142, 252);
}
.correct {
  background-color: rgb(123, 221, 123);
}
.incorrect {
  background-color: red;
}

.btn {
  margin: 0 5px;
}
</style>
