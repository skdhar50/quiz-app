<template>
<div class="ctr">
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar"></div>
            <div class="status">1 out of 3 questions answered</div>
        </div>
        <div class="single-question">
            <div class="question">Which of the following blood vessels carries deoxygenated blood?</div>
            <div class="answers">
                <div class="answer">Sample Answer 1</div>
                <div class="answer">Sample Answer 2</div>
                <div class="answer">Sample Answer 3</div>
                <div class="answer">Sample Answer 4</div>
            </div>
        </div>
    </div>
    <div class="result">
        <div class="title">You got sample result 1!</div>
        <div class="desc">
            Enter a short description here about the result.
        </div>
    </div>
    <button type="button" class="reset-btn">Reset</button>
</div>
  <!-- <button @click.prevent="load">Load</button>
  <ul>
    <li v-for="re in result" :key="re">
      <p v-html="re.question"></p>
    </li>
  </ul> -->
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      result: []
    };
  },
  methods: {
    async load() {
      try{
        const response = await axios.get("https://opentdb.com/api.php?amount=10&type=multiple");
        this.result = response.data.results;
        console.log(this.result)
      } catch(err) {
        console.log(err)
      }
    }
  }
}
</script>
