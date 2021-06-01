<template>
    <div class="result">
        <div class="title">
            <span v-if="wrongAnswers.length < 4">Great Job!!<br></span>
            <span v-else>Nice Try!!<br></span>
            You got {{ 10 - wrongAnswers.length }} out of 10!
        </div>
        <div class="desc" v-if="wrongAnswers.length > 0">
            <div class="correct" v-for="i in wrongAnswers" :key="i">
                <div class="que"> 
                    <p><b>Que:</b> <span v-html="questions[i]"></span></p>
                </div>
                <div class="ans"> 
                    <p><b>Answer:</b> <span v-html="correctAnswers[i]"></span></p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Result",
    props: [
        "wrongAnswers",
        "correctAnswers",
        "questions"
    ]

}
</script>

<style scoped>
.correct {
    border: 1px solid black;
    padding-left: 10px;
    margin-bottom: 5px;
    box-sizing: border-box;
}
</style>
