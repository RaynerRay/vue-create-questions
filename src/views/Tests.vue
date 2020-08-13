<!-- <template>
  <div id="tests">
    
     <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />

  <b-container class="by-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="getQuestions.length"
            :currentQuestion="getQuestions[index]"
            :next="next"
            :previous="previous"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>

    
  </div>
</template> -->

// <script>
// // @ is an alias to /src
// import Header from "@/components/Header.vue";
// import QuestionBox from "@/components/QuestionBox.vue";

// export default {
//   name: "Home",
//   components: {
//     Header,
//     QuestionBox,
//   },
//   data() {
//     return {
//       getQuestions: [],
//       index: 0,
//       numCorrect: 0,
//       numTotal: 0,
//     };
//   },
//   methods: {
//     next() {
//       this.index++;
//     },
//     increment(isCorrect) {
//       if (isCorrect) {
//         this.numCorrect++;
//       }
//       this.numTotal++;
//     },

//     previous() {
//       this.index--;
//     },
//   },

//   mounted: function() {
//     fetch("https://node-exam-api.herokuapp.com/questions", {
//       method: "get",
//     })
//       .then(response => {
//         return response.json();
//       })
//       .then(jsonData => {
//         let questions = jsonData;
//         this.getQuestions = questions;
//         console.log(questions);
//       });
//   },
// };
//
</script>

