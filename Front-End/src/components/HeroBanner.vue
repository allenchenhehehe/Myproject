<script setup>
defineProps({
    featured: Object,
})
</script>
<template>
    <div
        class="relative w-full h-screen bg-cover bg-center flex items-end mb-20"
        :style="{
            backgroundImage: `linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.3) 50%),
             url(${featured.imageUrl})`,
        }"
    >
        <div class="container mx-auto px-8 pb-32 z-10">
            <div class="max-w-2xl">
                <div class="flex items-center gap-4 mb-3">
                    <h1 class="text-5xl font-bold text-white">{{ featured.title }}</h1>
                    <div class="flex items-center bg-amber-500 px-3 py-1 rounded-md">
                        <Icon icon="mdi:star" class="text-yellow-300 mr-1" width="18" />
                        <span class="font-bold">{{ featured.rating }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
