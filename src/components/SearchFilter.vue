<template>
  <div class="flex gap-4 mb-4 relative">
    <!-- Search Input -->
    <input
      :value="search"
      @input="$emit('update:search', $event.target.value)"
      placeholder="🔍 Search ..."
      @focus="isSearchFocused = true"
      @blur="isSearchFocused = false"
      :class="[
        'px-2 py-1 rounded w-full border-2 outline-none',
        isSearchFocused ? 'border-green-400' : 'border-gray-300'
      ]"
    />

    <!-- Custom Dropdown -->
    <div class="relative w-40">
      <button
        @click="toggleDropdown"
        @blur="closeDropdown"
        :class="[
          'w-full border-2 px-2 py-1 rounded bg-white text-left flex justify-between items-center',
          isOpen ? 'border-green-400' : 'border-gray-300'
        ]"
      >
        {{ selectedLabel }}
        <svg class="w-4 h-4 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
        </svg>
      </button>

      <ul
        v-if="isOpen"
        class="absolute w-full mt-1 border rounded bg-white shadow z-10"
      >
        <li
          v-for="(label, value) in options"
          :key="value"
          @mousedown.prevent="selectOption(value)"
          class="px-2 py-1 hover:bg-green-300 cursor-pointer"
        >
          {{ label }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps(['search', 'source'])
const emit = defineEmits(['update:search', 'update:source'])

const isOpen = ref(false)
const isSearchFocused = ref(false)

const options = {
  '': 'All Sources',
  Facebook: 'Facebook',
  Instagram: 'Instagram',
  Google: 'Google',
  Website: 'Website',
}

const selectedLabel = computed(() => options[props.source] ?? 'All Sources')

function selectOption(value) {
  emit('update:source', value)
  isOpen.value = false
}

function toggleDropdown() {
  isOpen.value = !isOpen.value
}

function closeDropdown() {
  // Delay to allow click event to register before closing
  setTimeout(() => (isOpen.value = false), 150)
}
</script>
