<script setup lang="ts">
import datas from '../data/datas.json'
import Question from './Question.vue'
import Recap from './Recap.vue'

const { title, minimum_score, success_message, failure_message, questions } = datas
const number_of_questions = questions.length
const step = ref(1)
const current_question = computed(() => questions[step.value - 1])
const state = ref('quiz')

const answers = ref<(string | null)[]>(questions.map(() => null))

// ...

const addAnswer = (answer: string) => {
    answers.value[step.value - 1] = answer
    if (step.value === number_of_questions) {
        state.value = 'result'
    } else {
        step.value++
    }
}
</script>

<template>
    <div class="w-[800px] h-[500px] bg-red-200 flex flex-col justify-center items-start p-12 gap-12">
        <h1 class="text-3xl font-bold underline">{{ title }}</h1>
        <ProgressBar :value="step" :total="number_of_questions" />
        <Question
            :key="current_question.question"
            :question="current_question"
            v-if="state === 'quiz'"
            @addAnswer="addAnswer"
        />
        <Recap
            v-else-if="state === 'result'"
            :minimum_score="minimum_score"
            :success_message="success_message"
            :failure_message="failure_message"
            :questions="questions"
            :answers="answers"
        />
    </div>
</template>
