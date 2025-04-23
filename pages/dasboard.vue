<template>
      <div class="menu">
        <div class="col-lg-12">
            <h2 class="text-center my-4">DASBOARD</h2>
            <div class="position-relative">
              <div class="position-absolute top-50 start-0 translate-middle-y"><a href="" class="menu-item statistik">Statistik</a></div>
              <div class="position-absolute top-50 start-50 translate-middle"><NuxtLink to="/riwayatabsen"><a href="" class="menu-item riwayat1">Riwayat Absen</a></NuxtLink></div>
              <div class="position-absolute top-50 end-0 translate-middle-y"> <NuxtLink to="/menambahkan"> <a href="" class="menu-item riwayat2">Menambahkan</a></NuxtLink></div>
            </div>
      </div> 
      </div>
  </template>
  
  <script>
  export default {
    name: "Dashboard",
  };
  </script>
  
  <style scoped>
  .dashboard-container {
    background-color: #f0f0f0;
    min-height: 100px;
    padding: 10px;
  }

  .menu {
    padding-bottom: 18%;
  }
  .header {
    display: flex;
    align-items: center;
    background: #d3d3d3;
    padding: 10px;
  }
  .logo {
    width: 40px;
    height: 40px;
    margin-right: 10px;
  }
  .profile-button {
    margin-left: auto;
    background: none;
    border: none;
    cursor: pointer;
  }
  .profile-button img {
    width: 30px;
    height: 30px;
  }
  .menu {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 50px;
  }
  .menu-item {
    padding: 80px 100px;
    border-radius: 20px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
  }
  .statistik {
    background-color: #5a5af0;
    color: white;
    height: 200px;
    width: 30%;
  }
  .riwayat1 {
    background-color: #00ff00;
    color: white;
  }
  .riwayat2 {
    background-color: #ffeb3b;
    color: black;
  }
  </style>
  