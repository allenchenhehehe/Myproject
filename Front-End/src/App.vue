<script setup>
import { ref, onMounted } from 'vue'
import AppHeader from './components/AppHeader.vue'
import HeroBanner from './components/HeroBanner.vue'
const featuredContent = ref({
    title: '刺客567 feat. 雞大寶',
    rating: '8.7',
    imageUrl: '/hero.webp',
})
</script>

<template>
    <div class="min-h-screen bg-[#141414] text-white font-sans overflow-x-hidden">
        <AppHeader />
        <HeroBanner :featured="featuredContent" />
    </div>
</template>
