<template>
    <div class="mt-4 flex justify-center gap-2">
      <button
        v-for="page in pages"
        :key="page"
        :class="['px-3 py-1 rounded', currentPage === page ? 'bg-primary text-white' : 'bg-green-100']"
        @click="$emit('change', page)"
      >
        {{ page }}
      </button>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  
  // ✅ Destructure props directly
  const { currentPage, total, perPage } = defineProps()
  
  // ✅ Compute number of pages as an array
  const pages = computed(() => {
    const totalPages = Math.ceil(total / perPage)
    return Array.from({ length: totalPages }, (_, i) => i + 1)
  })
  </script>
  
  