<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{ width: `${ questionAnswered / 10 * 100 }%` }"></div>
            <div class="status">{{ questionAnswered }} out of 10 questions answered</div>
        </div>
        <transition-group name="fade">
            <div class="single-question" 
                v-for="(question, index) in questions" 
                :key="question"
                v-show="questionAnswered === index"
            >
                <div class="question" v-html="question"></div>
                <div class="answers" 
                    v-for="option in options[index]"
                    :key="option"
                    @click.prevent="selectAnswer(option)"
                >
                    <div class="answer" v-html="option"></div>
                </div>
            </div>
        </transition-group>
    </div>
</template>

<script>
export default {
    name: "Questions",
    props: [
        "questions",
        "options",
        "questionAnswered"
    ],
    emits: ["marked-question"],
    methods: {
        selectAnswer(option) {
            this.$emit("marked-question", option);
        }
    }
}
</script>
