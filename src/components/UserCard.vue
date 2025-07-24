<template>
    <div class="p-4 border border-b-cyan-400 shadow-cyan-300 hover rounded shadow bg-green-200">
      <h2 class="font-bold">{{ user.name }}</h2>
      <p>{{ user.email }}</p>
      <p class="text-sm text-white">Source: {{ user.source }}</p>
      <div class="mt-2 flex gap-2">
        <button class="bg-amber-400 text-white px-2 py-1 rounded" @click="$emit('delete', user.id)">Delete</button>
        <button class="bg-yellow-400 text-white px-2 py-1 rounded" @click="$emit('block', user.id)">Block</button>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps(['user'])
  </script>
  