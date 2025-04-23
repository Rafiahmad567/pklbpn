<template>
    <NuxtLink to="/dasboard" style="padding: 2%; margin: 2%;">
      <button class="back-button">⬅ Back</button>
    </NuxtLink>
  
    <div class="container">
      <h2 class="title">MENAMBAHKAN DATA BARU</h2>
      <div class="form-wrapper">
  
        <!-- Form 3 -->
        <div class="form-container">
          <form @submit.prevent="Data">
            <input v-model="form.asalsekolah" type="text" placeholder="Nama ...." class="input-field" />
            <button type="submit" class="submit-button">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient()
  
  const tes = ref({
    asalsekolah:"",
  });

  const Data = async () => {
    const { error } = await supabase.from("asalsekolah").insert([tes.value])
    if(!error) navigateTo("/")
    else throw error
  }
  </script>
  <!-- <script setup>
  const supabase = useSupabaseClient()
  
  const form = ref({
      nama: "",
  });
  
  
  const kirimData = async () => {
      console.log(form.value)
      const { error } = await supabase.from("nama").insert([form.value])
      if(!error)
      else throw error
  }
  
  </script> -->
  
  <style scoped>
  .back-button {
    background-color: white;
    padding: 10px 15px;
    border-radius: 9999px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  }
  
  .container {
    padding: 40px;
    background-color: #f8f8f8;
    border-radius: 10px;
    max-width: 1200px;
    margin: auto;
    text-align: center;
  }
  
  .title {
    font-size: 1.5rem;
    margin-bottom: 30px;
    font-weight: bold;
  }
  
  .form-wrapper {
    display: flex;
    justify-content: space-between;
    gap: 20px;
    flex-wrap: wrap;
  }
  
  .form-container {
    background-color: #ffffff;
    padding: 20px;
    border-radius: 15px;
    width: 30%;
    min-width: 250px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .input-field {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border-radius: 20px;
    border: 1px solid #ccc;
    background-color: rgba(200, 200, 200, 0.5);
    text-align: center;
  }
  
  .submit-button {
    padding: 10px 20px;
    border: none;
    border-radius: 20px;
    background-color: #6200ea;
    color: white;
    font-weight: bold;
    cursor: pointer;
    margin-top: 10px;
  }
  </style>
  