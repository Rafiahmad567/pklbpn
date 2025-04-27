<template>
  <NuxtLink to="/dasboard" style="padding: 2%; margin: 2%;" ><button @click="goBack" class="bg-white p-2 rounded-full shadow">
    ⬅ Back
  </button>
</NuxtLink>
    <div class="container">
      <div class="form-container">
        <div class="col-lg-12">
            <h2 class="text-center my-4">MENAMBAHKAN MURID</h2>
            <form  @submit.prevent="kirimData">
              <input v-model="form.jurusan" type="text" placeholder="Jurusan..." class="input-field highlight" />
              <button type="submit" class="submit-button">Submit</button>
            </form>
      </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient()

  const form = ref({
      jurusan: "",
  });
  const kirimData = async () => {
      console.log(form.value)
      const { error } = await supabase.from("jurusan").insert([form.value])
      if(!error) navigateTo("/menambahkan_sekolah")
      else throw error
  }
  </script>
  
  <style scoped>
  .container {
    text-align: center;
    padding: 80px;
    background-color: #f8f8f8;
    border-radius: 10px;
    width: 100%;
    max-width: 600px;
    margin: auto;
    position: relative;
  }
  .form-container {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .input-field {
    width: 80%;
    padding: 10px;
    margin: 10px 0;
    border-radius: 20px;
    border: 1px solid #ccc;
    background: rgba(200, 200, 200, 0.5);
    text-align: center;
  }
  .highlight {
    border: 2px solid blue;
  }
  .submit-button {
    padding: 10px 20px;
    border: none;
    border-radius: 20px;
    background-color: #6200ea;
    color: white;
    cursor: pointer;
    font-weight: bold;
    margin-top: 10px;
  }
  </style>
