<template>
  <div>
    <h1>ログイン</h1>
    <form @submit.prevent="login">
      <input v-model="email" type="email" placeholder="メールアドレス" />
      <input v-model="password" type="password" placeholder="パスワード" />
      <button type="submit">ログイン</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const email = ref('')
const password = ref('')
const error = ref('')

const login = async () => {
  try {
    const res = await axios.post('http://localhost:3000/api/v1/login', {
      email: email.value,
      password: password.value
    })
    alert(`ログイン成功: ${res.data.user.name}`)
  } catch (e) {
    alert(`ログイン失敗`)
  }
}
</script>
