<template>
    <div class="container">
      <div class="content">
        <h2>Anda telah berhasil</h2>
        <h3>mengisi absen</h3>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "AbsensiSuccess",
  };
  </script>
  
  <style scoped>
  .container {
    text-align: center;
    padding: 20px;
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
  </style>
  