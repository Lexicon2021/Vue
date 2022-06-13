<template>
    <div v-if="isQuizStarted">
        <h4>{{ operandLeft }} {{ operator }} {{ operandRight }}</h4>

        <button @click="selectAnswer(answer)" v-for="(answer, index) in answers" :key="index">{{ answer }}</button>
    </div>
    <div v-if="!isQuizStarted">
        <button @click="startQuiz">Start</button>
    </div>
  <button @click="$emit('onBack')">Back</button>
</template>

<script>
export default {
    props: ['operator'],
    data() {
        return {
            operandLeft: null,
            operandRight: null,
            isQuizStarted: false,
            answers: [],
            expectedAnswer: null
        }
    },
    methods: {
        startQuiz() {
            this.isQuizStarted = true;
            this.operandLeft = parseInt(Math.random() * 3);
            this.operandRight = parseInt(Math.random() * 3);

            const methods = {
                '+': (a , b) => a + b,
                '-': (a , b) => a - b,
                '/': (a , b) => a / b,
                '*': (a , b) => a * b,
            };

            const methodToUse = methods[this.operator];

            this.answers = [];

            for(let i = 0; i < 5; i++) {
                const answer = methodToUse( parseInt(Math.random() * 3),parseInt(Math.random() * 3))
                this.answers.push(answer);
            }

            const expectedAnswer = methodToUse(this.operandLeft, this.operandRight);
            console.log(expectedAnswer);
            this.answers[parseInt(Math.random() * this.answers.length)] = expectedAnswer;
            this.expectedAnswer = expectedAnswer;
        },

        selectAnswer(answerSelected) {
            if(answerSelected === this.expectedAnswer) {
                this.startQuiz();
            } else {
                alert('Wrong Answer');
            }
        }
    }
}
</script>

<style>

</style>