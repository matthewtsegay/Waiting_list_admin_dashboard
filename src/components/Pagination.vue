<template>
  <div class="mt-2 flex justify-center gap-1">
    <!-- Prev Button -->
    <button
      :disabled="currentPage <= 1"
      @click="$emit('change', currentPage - 1)"
      class="text-[10px] px-1.5 py-0.5 rounded-sm bg-green-500 text-white hover:bg-green-600 disabled:opacity-50"
    >
      ←
    </button>

    <!-- Page Numbers -->
    <button
      v-for="page in pages"
      :key="page"
      @click="$emit('change', page)"
      :class="[
        'text-[10px] px-1.5 py-0.5 rounded-sm border',
        currentPage === page
          ? 'bg-green-700 text-white border-green-700'
          : 'bg-white text-green-700 border-green-500 hover:bg-green-100'
      ]"
    >
      {{ page }}
    </button>

    <!-- Next Button -->
    <button
      :disabled="currentPage >= pages.length"
      @click="$emit('change', currentPage + 1)"
      class="text-[10px] px-1.5 py-0.5 rounded-sm bg-green-500 text-white hover:bg-green-600 disabled:opacity-50"
    >
      →
    </button>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  currentPage: Number,
  total: Number,
  perPage: Number
})

const pages = computed(() => {
  const totalPages = Math.ceil((props.total || 1) / (props.perPage || 1))
  return Array.from({ length: totalPages }, (_, i) => i + 1)
})
</script>
