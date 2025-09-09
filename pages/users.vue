<template>
  <div>
    <h1>ユーザー一覧</h1>

    <div v-if="loading">読み込み中...</div>
    <div v-if="error" style="color: red">{{ error }}</div>

    <ul v-if="!loading && !error">
      <li v-for="user in users" :key="user.id">
        {{ user.name }} - {{ user.email }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const users = ref([])
const loading = ref(false)
const error = ref(null)

onMounted(async () => {
  loading.value = true
  try {
    const res = await axios.get(`${import.meta.env.VITE_API_BASE_URL}/api/v1/users`)
    users.value = res.data
  } catch (e) {
    error.value = 'ユーザー一覧の取得に失敗しました'
    console.error(e)
  } finally {
    loading.value = false
  }
})
</script>
