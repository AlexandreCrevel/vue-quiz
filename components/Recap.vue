<script lang="ts" setup>
import { computed } from 'vue'

interface Question {
    correct_answer: string
    question: string
    choices: string[]
}

interface Props {
    minimum_score: number
    success_message: string
    failure_message: string
    questions: Question[]
    answers: (string | null)[]
}

const props = defineProps<Props>()

const score = computed(() => {
    if (!props.questions || !props.answers) return 0
    return props.questions.reduce((acc, question, index) => {
        if (props.answers[index] === question.correct_answer) {
            return acc + 1
        }
        return acc
    }, 0)
})

const has_won = computed(() => {
    return score.value >= props.minimum_score
})
</script>

<template>
    <div>
        <h1>Your score</h1>
        <p>{{ has_won ? props.success_message : props.failure_message }}</p>
        <p>{{ `${score}/${questions.length}` }}</p>
    </div>
</template>
