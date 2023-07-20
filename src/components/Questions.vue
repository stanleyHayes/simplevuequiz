<script>
export default {
    name: "Questions",
    props: ["questions", "questionsAnswered"],
    emits: ['question-answered'],
    methods: {
        selectAnswer(isCorrect) {
            this.$emit('question-answered', isCorrect)
        }
    }
}
</script>

<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{width: `${questionsAnswered / questions.length* 100}%`}"></div>
            <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
        </div>
        <transition-group name="fade">
            <div
                class="single-question"
                v-for="(question, index) in questions"
                v-show="questionsAnswered === index"
                :key="question.q">
                <div class="question">{{ question.q }}</div>
                <div class="answers">
                    <div
                        @click.prevent="selectAnswer(answer.is_correct)"
                        class="answer"
                        v-for="answer in question.answers"
                        :key="answer.text">
                        {{ answer.text }}
                    </div>
                </div>
            </div>
        </transition-group>
    </div>
</template>
