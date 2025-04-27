<template>
    <div class="container">
      <div class="content">
        <h2>LOGIN DI SINI</h2>
      </div>
      <div class="login-container">
        <input type="email" v-model="email" placeholder="Masukkan email..." class="input-field" />
        <input type="password" v-model="password" placeholder="password...." class="input-field" />
        <NuxtLink to="/dasboard" class="text-decoration-none">login</NuxtLink>
      </div>
    </div>
  </template>
  
  <script setup>
  definePageMeta({
    layout: 'login',
  })
  const client = useSupabaseClient()
  const email = ref("");
  const password = ref("");
  
  async function handleLogin() {
    console.log(email.value)
    console.log(password.value)
    const { data, error } = await client.auth.signInWithPassword({
      email: email.value,
      password: password.value
    })
    if (data) navigateTo('/dasboard')
  }
  </script>
  
  
  
  <style scoped>
  .container {
    text-align: center;
    padding: 100px;
    background-color: #f8f8f8;
    border-radius: 10px;
    width: 100%;
    max-width: 600px;
    margin: auto;
  }
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #ddd;
    padding: 10px;
    border-radius: 5px;
  }
  .logo {
    width: 40px;
    height: 40px;
  }
  .content {
    margin-top: 20px;
    font-size: 20px;
    font-weight: bold;
  }
  .login-container {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .input-field {
    width: 80%;
    padding: 10px;
    margin: 5px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  .login-button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    background-color: #ddd;
    cursor: pointer;
    font-weight: bold;
  }
  </style>
  