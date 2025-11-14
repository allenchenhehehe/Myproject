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

/*定義了所有可能的分類及其顯示名稱*/
const categories = [
    { key: 'expiring', name: '即將過期' },
    { key: 'vegetable', name: '蔬菜' },
    { key: 'protein', name: '蛋白質' },
    { key: 'seasoning', name: '調味料' },
    { key: 'oil', name: '油類' },
]

/*ingredients.value = {'蔬菜':[{id: '1',name: '洋蔥',quantity: 5。。。},{id: '4',name: '番茄',quantity: 5。。。}]}*/
const ingredients = ref(categorizeIngredients(mockData))
const expandedCategories = ref({
    expiring: false,
    vegetable: false,
    protein: false,
    seasoning: false,
    oil: false,
})
const isEditModalOpen = ref(false)
const editIngredient = ref(null)
/*輸入
[
  { name: '洋蔥', category: 'vegetable' },
  { name: '雞肉', category: 'protein' },
  { name: '雞蛋', category: 'protein' },
  { name: '番茄', category: 'vegetable' }
]

輸出
{
  vegetable: [{ name: '洋蔥' }, { name: '番茄' }],
  protein: [{ name: '雞肉' }, { name: '雞蛋' }]
}*/
function categorizeIngredients(data) {
    const categorized = {} // 步驟 A：建立空物件
    data.forEach((item) => {
        // 步驟 B：遍歷每個食材
        const category = item.category // 步驟 C：取出分類名稱
        // 步驟 D：檢查這個分類是否已經存在
        if (categorized[category] === undefined) {
            categorized[category] = [] // 步驟 E：不存在就建立空陣列
        }
        categorized[category].push(item) // 步驟 F：把食材加到對應分類的陣列
    })
    return categorized // 步驟 G：回傳轉換後的物件
}

function toggleCategory(key) {
    expandedCategories.value[key] = !expandedCategories.value[key]
}

function deleteIngredient(ingredientId) {
    if (confirm('確定要刪除這個食材嗎?')) {
        Object.keys(ingredients.value).forEach((category) => {
            ingredients.value[category] = ingredients.value[category].filter((item) => item.id !== ingredientId)
        })
    }
}
function openEditModal(ingredient) {
    editIngredient.value = ingredient
    isEditModalOpen.value = true
}
function closeEditModal() {
    editIngredient.value = null
    isEditModalOpen.value = false
}
function saveEdit(updatedData) {
    if (new Date(updatedData.purchased_date) > new Date(updatedData.expired_date)) {
        alert('購買日期不能晚於過期日期')
        return
    }
    // 找到要更新的食材，並更新它
    Object.keys(ingredients.value).forEach((category) => {
        const index = ingredients.value[category].findIndex((item) => item.id === editIngredient.value.id)

        if (index !== -1) {
            ingredients.value[category][index] = updatedData
        }
    })

    // 關閉 Modal
    closeEditModal()
}
</script>
<template>
    <div class="mt-28 max-w-4xl mx-auto px-4">
        <div class="flex justify-center items-center">
            <h1 class="text-4xl font-bold text-gray-800 mb-8">我的冰箱</h1>
        </div>

        <div class="space-y-4">
            <div v-for="category in categories" :key="category.key">
                <div class="bg-white rounded-lg shadow-md p-4 cursor-pointer" @click="toggleCategory(category.key)">
                    <div class="flex justify-between items-center p-2">
                        <span>
                            {{ category.name }}
                        </span>
                        <span>
                            {{ ingredients[category.key]?.length || 0 }}
                        </span>
                    </div>
                </div>
                <div v-if="expandedCategories[category.key]" class="border-t border-gray-500 space-y-4 p-4">
                    <div
                        v-for="ingredient in ingredients[category.key]"
                        :key="ingredient.id"
                        class="bg-gray-50 rounded p-3 flex justify-between items-center"
                    >
                        <div class="p-2 space-y-1">
                            <div>{{ ingredient.name }}</div>
                            <div>{{ ingredient.quantity }}{{ ingredient.unit }}</div>
                        </div>
                        <div class="flex gap-2">
                            <button @click="openEditModal(ingredient)" class="bg-blue-500 text-white px-3 py-1 rounded text-sm">編輯</button>
                            <button @click="deleteIngredient(ingredient.id)" class="bg-red-500 text-white px-3 py-1 rounded text-sm">刪除</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- 編輯 Modal -->
    <div
        v-if="isEditModalOpen"
        class="fixed inset-0 bg-opacity-30 flex items-center justify-center z-50"
        style="background-color: rgba(0, 0, 0, 0.2)"
    >
        <div class="bg-white rounded-lg p-6 w-96">
            <h2 class="text-2xl font-bold mb-4">編輯食材</h2>

            <div v-if="editIngredient" class="space-y-4">
                <div>
                    <label class="block font-bold mb-2">食材名稱</label>
                    <input type="text" :value="editIngredient.name" disabled class="w-full border p-2 bg-gray-100" />
                </div>

                <div>
                    <label class="block font-bold mb-2">數量</label>
                    <input type="number" v-model.number="editIngredient.quantity" class="w-full border p-2" />
                </div>

                <div>
                    <label class="block font-bold mb-2">購買日期</label>
                    <input type="date" v-model="editIngredient.purchased_date" class="w-full border p-2" />
                </div>

                <div>
                    <label class="block font-bold mb-2">過期日期</label>
                    <input type="date" v-model="editIngredient.expired_date" class="w-full border p-2" />
                </div>
            </div>

            <div class="flex gap-2 mt-6">
                <button @click="saveEdit(editIngredient)" class="flex-1 bg-blue-500 text-white px-4 py-2 rounded">確認</button>
                <button @click="closeEditModal()" class="flex-1 bg-gray-500 text-white px-4 py-2 rounded">取消</button>
            </div>
        </div>
    </div>
</template>
