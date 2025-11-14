<script setup>
import { ref, computed, defineEmits } from 'vue'
const emit = defineEmits(['gotorecipedetail'])
const mockRecipes = [
    {
        id: '1',
        title: '番茄炒蛋',
        description: '簡單快手菜，營養豐富',
        dificulty: 3,
        coocking_time: 12,
        step: '1. 打蛋\n 2. 炒蛋\n 3. 加番茄',
        creator_id: 'system',
        is_public: true,
        image_url: '/TomatoEgg.webp',
        ingredients: [
            { ingredient_id: 4, ingredient_name: '番茄', quantity: 2, unit: '個' },
            { ingredient_id: 3, ingredient_name: '雞蛋', quantity: 3, unit: '個' },
        ],
    },
    {
        id: '2',
        title: '洋蔥炒蛋',
        description: '經典家常菜，做法簡單',
        dificulty: 2,
        coocking_time: 20,
        step: '1.切洋蔥\n 2. 炒洋蔥\n 3. 打蛋炒',
        creator_id: 'system',
        is_public: true,
        image_url: '/TomatoEgg.webp',
        ingredients: [
            { ingredient_id: 1, ingredient_name: '洋蔥', quantity: 1, unit: '個' },
            { ingredient_id: 3, ingredient_name: '雞蛋', quantity: 2, unit: '個' },
        ],
    },
    {
        id: '3',
        title: '威靈頓牛排',
        description: '高手才能作的菜，做法稍嫌複雜',
        dificulty: 5,
        coocking_time: 60,
        step: '1.小火煎牛排\n2. 烤麵包\n3. 牛排塞進麵包裡',
        creator_id: 'system',
        is_public: true,
        image_url: '/TomatoEgg.webp',
        ingredients: [
            { ingredient_id: 5, ingredient_name: '牛排', quantity: 1, unit: '塊' },
            { ingredient_id: 6, ingredient_name: '奶油', quantity: 1, unit: '塊' },
        ],
    },
]
const recipes = ref(mockRecipes)
const filterByMyIngredient = ref(false) //要不要根據我的食材篩選
const selectByCookingTime = ref('all') //根據時長
const filterRecipes = computed(() => {
    if (selectByCookingTime.value === 'all') {
        return recipes.value
    } else if (selectByCookingTime.value === '15') {
        return recipes.value.filter((recipe) => {
            return recipe.coocking_time <= 15
        })
    } else if (selectByCookingTime.value === '30') {
        return recipes.value.filter((recipe) => {
            return recipe.coocking_time <= 30
        })
    } else if (selectByCookingTime.value === '60') {
        return recipes.value.filter((recipe) => {
            return recipe.coocking_time >= 60
        })
    }
})
function handleCookRecipe(recipe) {
    emit('gotorecipedetail', recipe)
}
</script>
<template>
    <div class="mt-28 max-w-7xl mx-auto px-4">
        <div class="flex justify-center items-center"><h1 class="mb-8 text-4xl">想做些甚麼料理嗎!</h1></div>

        <div class="bg-white p-4 rounded-lg mb-4 shadow-md flex flex-col items-center justify-center space-y-6">
            <div>
                <h3 class="text-lg font-bold text-gray-500">食譜類型</h3>
            </div>

            <div class="flex gap-3">
                <button
                    @click="filterByMyIngredient = false"
                    :class="!filterByMyIngredient ? 'text-white bg-amber-500' : 'text-gray-200 bg-gray-700'"
                    class="rounded font-semibold px-3 py-2 cursor-pointer"
                >
                    所有食譜
                </button>
                <button
                    @click="filterByMyIngredient = true"
                    :class="filterByMyIngredient ? 'text-white bg-amber-500' : 'text-gray-200 bg-gray-700'"
                    class="rounded font-semibold px-3 py-2 cursor-pointer"
                >
                    根據我的食材
                </button>
            </div>

            <div>
                <h3 class="text-lg font-bold text-gray-500">烹飪時間</h3>
            </div>

            <div class="flex gap-2">
                <button
                    @click="selectByCookingTime = 'all'"
                    :class="selectByCookingTime == 'all' ? 'text-white bg-amber-500' : 'text-gray-300 bg-gray-700'"
                    class="rounded font-semibold px-3 py-1 cursor-pointer"
                >
                    所有
                </button>
                <button
                    @click="selectByCookingTime = '15'"
                    :class="selectByCookingTime == '15' ? 'text-white bg-amber-500' : 'text-gray-300 bg-gray-700'"
                    class="rounded font-semibold px-3 py-1 cursor-pointer"
                >
                    小於15分鐘
                </button>
                <button
                    @click="selectByCookingTime = '30'"
                    :class="selectByCookingTime == '30' ? 'text-white bg-amber-500' : 'text-gray-300 bg-gray-700'"
                    class="rounded font-semibold px-3 py-1 cursor-pointer"
                >
                    小於30分鐘
                </button>
                <button
                    @click="selectByCookingTime = '60'"
                    :class="selectByCookingTime == '60' ? 'text-white bg-amber-500' : 'text-gray-300 bg-gray-700'"
                    class="rounded font-semibold px-3 py-1 cursor-pointer"
                >
                    60分鐘以上
                </button>
            </div>
        </div>

        <div class="flex flex-wrap gap-6 mt-8">
            <div
                v-for="recipe in filterRecipes"
                :key="recipe.id"
                class="bg-white rounded-lg overflow-hidden shadow-md w-[calc(50%-12px)] shrink-0 flex"
            >
                <img :src="recipe.image_url" :alt="recipe.title" class="w-1/3 object-cover h-48" />
                <div class="flex flex-col justify-between flex-1 p-4">
                    <div>
                        <h3 class="font-bold text-xl mb-2">{{ recipe.title }}</h3>
                        <p class="text-sm text-gray-500 mb-4">{{ recipe.description }}</p>
                    </div>

                    <div class="flex justify-between mb-3">
                        <span class="text-sm">難度:&nbsp;&nbsp;{{ recipe.dificulty }}/5</span>
                        <span class="text-sm">大約:&nbsp;&nbsp;{{ recipe.coocking_time }}分</span>
                    </div>
                    <div class="flex gap-2">
                        <button @click="handleCookRecipe(recipe)" class="w-full bg-amber-300 text-black text-sm px-3 py-2 rounded cursor-pointer">
                            我要做!
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
