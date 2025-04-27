<template>
  <div class="menu-container">
    <h2 class="title">DASBOARD</h2>
    <div class="menu">
      <NuxtLink to="/riwayatabsen" class="menu-item riwayat1">Riwayat Absen</NuxtLink>
      <NuxtLink to="/menambahkan" class="menu-item riwayat2">Menambahkan</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dashboard",
};
</script>

<style scoped>
/* Membungkus semua konten */
.menu-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 80vh;
  text-align: center;
}

/* Judul */
.title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 2rem;
}

/* Menu item */
.menu {
  display: flex;
  gap: 2rem;
}

.menu-item {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px 100px;
  border-radius: 20px;
  font-size: 18px;
  font-weight: bold;
  text-decoration: none;
}

/* Warna background masing-masing */
.riwayat1 {
  background-color: #00ff00;
  color: white;
}

.riwayat2 {
  background-color: #ffeb3b;
  color: black;
}
</style>

  