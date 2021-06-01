<template>
<div class="ctr">
    
    <questions />
    <result />
    
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
import Questions from "./components/Questions.vue";
import Result from "./components/result.vue";

export default {
  name: "App",
  components: { 
    Questions,
    Result
  },
  
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
