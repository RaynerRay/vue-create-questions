<template>
    <div>
    <h1>Create Questions</h1>
    <div class="container">
        <b-col sm="12">
            <b-form-select v-model="selected" :options="options"></b-form-select>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="text" placeholder="Question"></b-form-input>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="answer1" placeholder="Answer 1"></b-form-input>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="answer2" placeholder="Answer 2"></b-form-input>
        </b-col><br>
        <b-col sm="12">
           <b-form-input v-model="answer3" placeholder="Answer 3"></b-form-input>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="correctAnswer" placeholder="correctAnswer"></b-form-input>
        </b-col><br>
        
        <b-col sm="12">
            <b-form-textarea
            id="textarea"
            v-model="explanation"
            placeholder="Question Explanation..."
            rows="3"
            max-rows="6"
        >
        </b-form-textarea><br>
        <b-button variant="info" @click="addToApi()">Submit</b-button>
        </b-col>
    </div>

    
        
    </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      selected: null,
      options: [
        { value: null, text: "Select a Subject" },
        { value: "5f35652808e46d00173fbb70", text: "Human Peformance" },
        {
          value: "5f35646708e46d00173fbb69",
          text: "Operation Procedures (IR)",
        },
        { value: "5f35649d08e46d00173fbb6a", text: "Navigation" },
        {
          value: "5f3564ba08e46d00173fbb6b",
          text: "Instruments and Electronics",
        },
        { value: "5f3564cf08e46d00173fbb6c", text: "Radio Aids" },
        {
          value: "5f3564e308e46d00173fbb6d",
          text: "Flight Planning and Performance",
        },
        { value: "5f3564fb08e46d00173fbb6e", text: "Air Law" },
        { value: "5f35650d08e46d00173fbb6f", text: "Aviation Meteorology" },
        {
          value: "5f35653e08e46d00173fbb71",
          text: "General Navigation and Plotting",
        },
        {
          value: "5f35656308e46d00173fbb72",
          text: "Aircraft Technical and General",
        },
      ],

      text: "",
      descriptionImage: "",
      answer1: "",
      answer1Image: "",
      answer2: "",
      answer2Image: "",
      answer3: "",
      answer3Image: "",
      correctAnswer: "",
      correctAnswerImage: "",
      explanation: "",
      explanationImage: "",
    };
  },
  methods: {
    addToApi() {
      axios
        .post("https://pilot-trainer.herokuapp.com/questions", {
          description: [
            {
              text: this.text,
              image: this.descriptionImage,
            },
          ],
          alternatives: [
            {
              text: this.answer1,
              image: this.answer1Image,
            },
            {
              text: this.answer2,
              image: this.answer2Image,
            },
            {
              text: this.answer3,
              image: this.answer3Image,
            },

            {
              text: this.correctAnswer,
              image: this.correctAnswerImage,
              isCorrect: true,
            },
          ],
          explanation: [
            {
              text: this.explanation,
              image: this.explanationImage,
            },
          ],
          subjects: [this.selected],
        })
        .then(response => {
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
</style>
