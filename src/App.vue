<template>
<div class="ctr">
    
    <div class="start" v-if="!isPlaying">
      <h1>Are you Ready?</h1>
      <h3>You have to answer 10 Questions!</h3>
      <button type="button" class="reset-btn" @click.prevent="load">
        Start
      </button>
    </div>
    <div class="main" v-else>
      <transition name="fade" mode="out-in">
        <questions 
          v-if="questionAnswered < 10" 
          :questions="questions"
          :options="options"
          :questionAnswered="questionAnswered"
          @marked-question="markedQuestion"
        />
        <result 
            v-else
            :wrongAnswers="wrongAnswers"
            :questions="questions"
            :correctAnswers="correctAnswers"
        />
      </transition>
    </div>
    
    <button 
      type="button"
      class="reset-btn"
      v-if="questionAnswered === 10"
      @click.prevent="resetAll"
    >
      Try Again
    </button>
</div>
</template>

<script>
import axios from "axios";
import Questions from "./components/Questions.vue";
import Result from "./components/result.vue";

export default {
  name: "App",
  components: { 
    Questions,
    Result,
  },
  
  data() {
    return {
      result: [],
      questionAnswered: 0,
      options: [],
      questions: [],
      correctAnswers: [],
      wrongAnswers: [],
      isPlaying: false,
    };
  },
  methods: {
    async load() {
      try{
        const response = await axios.get("https://opentdb.com/api.php?amount=10&type=multiple");
        this.result = response.data.results;
        for( let i = 0; i < 10; i++ ) {
          this.questions[i] = this.result[i].question;
          this.correctAnswers[i] = this.result[i].correct_answer;
          this.options[i] = [...this.result[i].incorrect_answers, this.result[i].correct_answer];

          for (let j = 3; j > 0; j--) {
            for(let l = 0; l < 100; l++) {
              let k = Math.floor(Math.random() * (j + 1));
              [this.options[i][j], this.options[i][k]] = [this.options[i][k], this.options[i][j]];
            }
          }
        }
      } catch(err) {
        console.log(err)
      }

      this.isPlaying = !this.isPlaying;
    },

    markedQuestion(option) {
      if( this.correctAnswers[this.questionAnswered] !== option ) {
        this.wrongAnswers.push(this.questionAnswered);
      }
      this.questionAnswered++;
    },

    resetAll() {
      this.result = [];
      this.questionAnswered = 0;
      this.options = [];
      this.questions = [];
      this.correctAnswers = [];
      this.wrongAnswers = [];
      this.isPlaying = false;
    }
  }
}
</script>
