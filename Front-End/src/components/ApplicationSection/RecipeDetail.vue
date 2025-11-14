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

        <div v-if="props.recipe" class="bg-white rounded-b-lg p-6 gap-6 flex shadow-md">
            <img :src="props.recipe.image_url" :alt="props.recipe.title" class="w-1/3 object-cover h-full" />
            <div class="flex flex-col flex-1 gap-6">
                <div class="text-gray-500 border-b border-gray-200 pb-4">
                    <h2 class="mb-6 text-4xl font-bold">{{ props.recipe.title }}</h2>
                    <div class="flex justify-between">
                        <span>烹飪時長 : 約{{ props.recipe.coocking_time }}分</span>
                        <span>創作者 : {{ props.recipe.creator_id }}</span>
                    </div>
                </div>

                <div class="border-b border-gray-200 pb-4">
                    <h3 class="text-lg font-bold mb-4">準備食材 (一人份)</h3>
                    <div class="space-y-2 mb-4">
                        <div v-for="ingredient in props.recipe.ingredients" :key="ingredient.id" class="flex justify-between">
                            <span>{{ ingredient.ingredient_name }}</span>
                            <span>{{ ingredient.quantity }}{{ ingredient.unit }}</span>
                        </div>
                    </div>
                    <div class="flex gap-4 items-center">
                        <div class="flex-1">
                            <p class="text-red-600">缺少...食材</p>
                        </div>
                        <button class="w-1/3 mt-4 bg-gray-500 text-white py-2 rounded">加入購物清單</button>
                    </div>
                </div>
                <div>
                    <h3 class="text-lg mb-4 font-bold">詳細步驟</h3>
                    <p class="whitespace-pre-line text-gray-700">{{ props.recipe.step }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
