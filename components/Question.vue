<script lang="ts" setup>
import { defineProps } from 'vue'

type question = { question: string; choices: string[]; correct_answer: string }

const props = defineProps({
    question: {
        type: Object as () => question,
        required: true,
    },
    addAnswer: Function,
})
const answer = ref(null)
const emits = defineEmits(['addAnswer'])
</script>
<template>
    <div class="w-full">
        <h3 class="text-2xl mb-4">{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in question.choices">
                <label for="`answer${index}`">
                    <input
                        type="radio"
                        name="answer"
                        :value="choice"
                        id="`answer${index}`"
                        class="mr-2"
                        v-model="answer"
                    />
                    {{ choice }}
                </label>
            </li>
        </ul>
        <button
            :disabled="!answer"
            @click="emits('addAnswer', answer)"
            class="disabled:opacity-50 bg-yellow-500 hover:bg-yellow-700 text-white font-bold mt-2 py-3 px-4 rounded ml-auto block"
        >
            Next Question
        </button>
    </div>
</template>
