<script setup></script>
<template>
    <div class="space-y-6 pt-24">
        <h2 class="text-2xl font-bold text-gray-800 pb-2 pl-2 mb-4">歡迎使用 Pantry Pilot！</h2>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- 卡片 2: 庫存概覽 -->
            <div class="bg-blue-50 p-6 rounded-xl shadow-md border-l-4 border-blue-500 transition hover:shadow-lg">
                <h3 class="font-semibold text-xl text-blue-600 mb-2">🧊 冰箱概覽</h3>
                <p class="text-gray-700">冰箱內共有 <span class="font-bold">3 類 12 項</span> 食材。</p>
                <button class="mt-3 text-sm font-medium text-blue-500 hover:text-blue-700">管理庫存</button>
            </div>

            <!-- 卡片 3: 食譜推薦 -->
            <div class="bg-yellow-50 p-6 rounded-xl shadow-md border-l-4 border-yellow-500 transition hover:shadow-lg">
                <h3 class="font-semibold text-xl text-yellow-700 mb-2">👨‍🍳 智能食譜</h3>
                <p class="text-gray-700">有 <span class="font-bold">5 個</span> 食譜可以使用您目前所有食材。</p>
                <button class="mt-3 text-sm font-medium text-yellow-700 hover:text-yellow-900">探索食譜</button>
            </div>
        </div>

        <div class="mt-8 p-6 bg-white rounded-xl shadow-lg">
            <h3 class="text-xl font-semibold mb-3">待辦事項與最新動態</h3>
            <p class="text-gray-600">這是應用程式的中央控制台，將來會顯示所有重要資訊的彙整。</p>
        </div>
    </div>
</template>
