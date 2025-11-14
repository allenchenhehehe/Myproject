<script setup>
import { ref, defineProps, defineEmits } from 'vue'
const recipe = ref(null)
const emit = defineEmits(['handlegoback'])
const props = defineProps({
    recipe: Object,
})
function handleGoBack() {
    emit('handlegoback')
}
</script>
<template>
    <div class="mt-28 max-w-7xl mx-auto px-4">
        <div class="flex justify-center items-center relative">
            <h1 class="mb-8 text-4xl">食譜詳情</h1>
            <button @click="handleGoBack" class="mb-6 px-4 py-2 bg-gray-300 text-gray-700 rounded font-semibold absolute right-0 cursor-pointer">
                返回列表
            </button>
        </div>

        <div v-if="props.recipe" class="bg-white rounded-b-lg p-4 mb-6 shadow-md">
            <div class="flex justify-between text-gray-500 border-b border-gray-200 mb-6 p-4">
                <h2 class="mb-4 text-2xl">{{ props.recipe.title }}</h2>
                <div>
                    <span class="m-4">烹飪時長 : 約{{ props.recipe.coocking_time }}分</span>
                    <span class="m-4">創作者 : {{ props.recipe.creator_id }}</span>
                </div>
            </div>
            <div class="border-b border-gray-200 mb-4 flex flex-col items-center justify-center">
                <h3 class="text-lg font-bold mb-4">準備食材 (一人份)</h3>
                <div class="space-y-2">
                    <div v-for="ingredient in props.recipe.ingredients" :key="ingredient.id" class="mb-4">
                        <span>{{ ingredient.ingredient_name }}</span>
                        <span>{{ ingredient.quantity }}{{ ingredient.unit }}</span>
                    </div>
                </div>
            </div>

            <div class="mb-6 pb-6 border-b border-gray-200 flex justify-center flex-col items-center">
                <h3 class="text-lg mb-4 font-bold">詳細步驟</h3>
                <p class="whitespace-pre-line text-gray-700">{{ props.recipe.step }}</p>
            </div>
        </div>
    </div>
</template>
