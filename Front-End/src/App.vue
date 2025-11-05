<script setup>
import { ref, onMounted } from 'vue'
import AppHeader from './components/AppHeader.vue'
import HeroBanner from './components/HeroBanner.vue'
const featuredContent = ref({
    title: 'StrangerThing',
    yaer: 1987,
    rating: decription,
})
</script>

<template>
    <div class="min-h-screen bg-[#141414] text-white font-sans overflow-x-hidden">
        <AppHeader />
        <HeroBanner :featured="featuredContent" />
    </div>
</template>
