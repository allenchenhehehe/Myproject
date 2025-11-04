<script setup>
import { ref } from 'vue'
const navLinks = ref([
  { name: 'Home', active: 'true' },
  { name: 'TVSeries' },
  { name: 'Animations' },
  { name: 'Movies' },
  { name: 'New & Popular' },
])
</script>

<template>
  <header
    class="fixed top-0 w-full max-w-screen overflow-x-hidden z-50 bg-black/90 backdrop-blur-sm"
  >
    <div class="px-8 py-4 relative">
      <div class="absolute left-8 top-1/2 -translate-y-1/2 z-10">
        <div class="text-3xl font-bold text-[#F79C0F]">5Dmax</div>
      </div>

      <div class="flex justify-center">
        <nav class="hidden md:flex items-center space-x-6 text-sm">
          <a
            href="#"
            v-for="link in navLinks"
            :key="link.name"
            :class="{
              'text-white font-bold': link.active,
              'text-[#757575] hover:text-white': !link.active,
            }"
          >
            {{ link.name }}
          </a>
        </nav>
      </div>

      <div class="absolute right-8 top-1/2 -translate-y-1/2 z-10">
        <div class="flex items-center space-x-4">
          <button class="text-white">
            <Icon icon="ic:round-search" class="w-6 h-6" />
          </button>
        </div>
      </div>
    </div>
  </header>
</template>
