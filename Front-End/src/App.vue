<script setup>
import { ref, onMounted } from 'vue'
import AppHeader from './components/AppHeader.vue'
import Login from "./components/Login.vue"
const featuredContent = ref({
    title: '刺客伍陸柒 feat. 雞大寶',
    rating: '8.7',
    imageUrl: '/hero.webp',
    year: '1998',
    seasons:'4Seasons'
})
</script>

<template>
    <div class="min-h-screen bg-[#757575] text-white font-sans overflow-x-hidden">
        <Login/>
    </div>
</template>
