<template>
  <div
    class="w-full max-w-xs h-64 p-5 bg-green-200 border border-green-500 rounded-lg flex flex-col justify-between 
           hover:bg-green-300 hover:shadow-lg hover:shadow-green-500 hover:scale-95 transition-all duration-300 ease-in-out"
  >
    <div>
      <h2 class="text-lg font-bold text-green-600 mb-1">{{ user.name }}</h2>
      <p class="text-gray-700">{{ user.email }}</p>
      <p class="text-sm font-bold text-gray-400 mt-1">Source: {{ user.source }}</p>
    </div>

    <div class="mt-4 flex justify-center gap-3">
      <button
        class="border border-red-600 bg-red-500 text-sm px-4 py-2 rounded hover:bg-red-600 text-white transition"
        @click="$emit('delete', user.id)"
      >
        Delete
      </button>
      <button
        class="border border-orange-500 text-orange-500 text-sm px-4 py-2 rounded hover:bg-orange-500 hover:text-white transition"
        @click="$emit('block', user.id)"
      >
        Block
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps(['user'])
</script>
