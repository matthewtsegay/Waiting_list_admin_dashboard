<template>
    <div class="flex gap-4 mb-4">
      <input
        :value="search"
        @input="$emit('update:search', $event.target.value)"
        placeholder="Search by name..."
        class=" px-2 py-1 rounded w-full border-2 border-b-cyan-400"
      />
      <select
        :value="source"
        @change="$emit('update:source', $event.target.value)"
        class="border px-2 py-1 rounded border-b-cyan-400"
      >
        <option value="">All Sources</option>
        <option>Facebook</option>
        <option>Instagram</option>
        <option>Google</option>
        <option>Website</option>
      </select>
    </div>
  </template>
  
  <script setup>
  defineProps(['search', 'source'])
  defineEmits(['update:search', 'update:source'])
  </script>
  