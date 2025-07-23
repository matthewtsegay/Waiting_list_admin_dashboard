<template>
    <div class="mt-8">
      <h2 class="text-lg font-bold mb-2">Signups by Source</h2>
      <div class="w-full bg-green-100 rounded p-4">
        <div
          v-for="(count, source) in counts"
          :key="source"
          class="flex justify-between border-b py-1"
        >
          <span>{{ source }}</span>
          <span>{{ count }}</span>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  const props = defineProps(['users'])
  
  const counts = computed(() => {
    const result = {}
    props.users.forEach(user => {
      result[user.source] = (result[user.source] || 0) + 1
    })
    return result
  })
  </script>
  