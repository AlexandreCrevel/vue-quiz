<script lang="ts" setup>

const props = defineProps({
    value: {
        type: Number,
        default: 1
    },
    total: {
        type: Number,
        default: 5
    }
})
const percent = computed(() => props.value / props.total * 100)
</script>

<template>
    <div class="flex flex-col items-start gap-2 w-96">
        <span class="w-32">{{`Step ${value}/${total}` }}</span>
        <progress class="w-full bg-gray-200 rounded-full h-2.5 dark:bg-gray-700" :value="value" :max="total - 1"></progress>

    </div>
</template>