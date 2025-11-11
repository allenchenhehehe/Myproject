<script setup>
import { ref } from 'vue'

const mockData = [
    {
        id: '1',
        name: '洋蔥',
        category: 'vegetable',
        quantity: 5,
        unit: '個',
        purchased_date: '2025-11-03',
        expired_date: '025-11-12',
        days_left: 2,
        is_expired: true,
    },
    {
        id: '2',
        name: '雞肉',
        category: 'protein',
        quantity: 200,
        unit: '克',
        purchased_date: '2025-11-05',
        expired_date: '025-11-11',
        days_left: 1,
        is_expired: true,
    },
    {
        id: '3',
        name: '雞蛋',
        category: 'protein',
        quantity: 2,
        unit: '顆',
        purchased_date: '2025-11-08',
        expired_date: '025-11-12',
        days_left: 2,
        is_expired: true,
    },
    {
        id: '4',
        name: '番茄',
        category: 'vegetable',
        quantity: 5,
        unit: '個',
        purchased_date: '2025-11-03',
        expired_date: '025-11-30',
        days_left: 20,
        is_expired: false,
    },
]
const categories = [
    { key: 'expiring', name: '即將過期' },
    { key: 'vegetable', name: '蔬菜' },
    { key: 'protein', name: '蛋白質' },
    { key: 'seasoning', name: '調味料' },
    { key: 'oil', name: '油類' },
]

const ingredients = ref(categorizeIngredients(mockData))

function categorizeIngredients(data) {
    const categorized = {}
    data.forEach((item) => {
        const category = item.category
        if (categorized[category] === undefined) {
            categorized[category] = []
        }
        categorized[category].push(item)
    })
    return categorized
}
</script>
<template>
    <div class="mt-28 max-w-4xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-gray-800 mb-8">我的冰箱</h1>
        <div class="space-y-4">
            <div v-for="category in categories" :key="category.key">
                <div class="bg-white rounded-lg shadow-md p-4">
                    <div class="flex justify-between items-center">
                        <span>
                            {{ category.name }}
                        </span>
                        <span>
                            {{ ingredients[category.key]?.length || 0 }}
                        </span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
