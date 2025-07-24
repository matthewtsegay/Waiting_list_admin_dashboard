<template>
    <div class="min-h-screen w-full border-4 border-green-500 shadow-green-2 bg-green-50 text-gray-800 p-6">
      <h1 class="text-green-400 text-2xl font-bold text-primary mb-6"> Admin Dashboard</h1>
      <SearchFilter
        :search="searchQuery"
        :source="filterSource"
        @update:search="val => searchQuery = val"
        @update:source="val => filterSource = val"
     />
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-4 my-4">
        <UserCard
          v-for="user in paginatedUsers"
          :key="user.id"
          :user="user"
          @delete="deleteUser"
          @block="blockUser"
        />
      </div>
  
      <Pagination
        :current-page="currentPage"
        :total="filteredUsers.length"
        :per-page="perPage"
        @change="page => currentPage = page"
      />
  
      <div class="flex gap-4 mt-6">
        <button class="bg-green-400 hover:bg-green-500 text-white px-4 py-2 rounded" @click="exportCSV(filteredUsers)">
          Export CSV
        </button>
      </div>
  
      <SignupChart :users="users" />
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import mockData from '../mockData.js'
  import SearchFilter from '../components/SearchFilter.vue'
  import UserCard from '../components/UserCard.vue'
  import Pagination from '../components/Pagination.vue'
  import SignupChart from '../components/SignupChart.vue'
  import { exportCSV } from '../utils/exportCSV.js'
  
  const users = ref(mockData)
  const searchQuery = ref('')
  const filterSource = ref('')
  const currentPage = ref(1)
  const perPage = 6
  
  const filteredUsers = computed(() => {
    return users.value.filter(user =>
      user.name.toLowerCase().includes(searchQuery.value.toLowerCase()) &&
      (filterSource.value === '' || user.source === filterSource.value)
    )
  })
  
  const paginatedUsers = computed(() => {
    const start = (currentPage.value - 1) * perPage
    return filteredUsers.value.slice(start, start + perPage)
  })
  
  function deleteUser(id) {
    if (confirm("Are you sure to delete this user?")) {
      users.value = users.value.filter(user => user.id !== id)
    }
  }
  
  function blockUser(id) {
    if (confirm("Block this user?")) {
      alert(`User ${id} blocked (mock action)`)
    }
  }
  </script>
  