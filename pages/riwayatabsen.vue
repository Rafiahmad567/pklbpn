<template>
    <div class="min-h-screen bg-gray-100">
      <!-- Header -->
      <div class="bg-gray-300 p-4 flex items-center gap-4">
        <NuxtLink to="/dasboard"><button @click="goBack" class="bg-white p-2 rounded-full shadow">
          ⬅ Back
        </button>
    </NuxtLink>
        <h1 class="text-2xl font-semibold">Riwayat Absensi</h1>
      </div>
  
      <!-- Tabel Riwayat -->
      <div class="p-4">
        <table class="w-full border-collapse">
          <thead>
            <tr>
              <th class="border border-gray-300 bg-blue-200 p-2 text-left">Tanggal</th>
              <th class="border border-gray-300 bg-blue-200 p-2 text-left">Waktu Masuk</th>
              <th class="border border-gray-300 bg-blue-200 p-2 text-left">Waktu Keluar</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(absen, index) in riwayat" :key="index" :class="index % 2 === 0 ? 'bg-white' : 'bg-gray-200'">
              <td class="border border-gray-300 p-2">{{ absen.tanggal }}</td>
              <td class="border border-gray-300 p-2">{{ absen.masuk }}</td>
              <td class="border border-gray-300 p-2">{{ absen.keluar }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        riwayat: [
          { tanggal: "2025-04-20", masuk: "08:00", keluar: "16:00" },
          { tanggal: "2025-04-19", masuk: "08:10", keluar: "16:05" },
          { tanggal: "2025-04-18", masuk: "08:05", keluar: "15:55" },
          // Tambah data lain sesuai kebutuhan
        ],
      };
    },
    methods: {
      goBack() {
        // Navigasi balik, sesuaikan dengan routing aplikasi kamu
        window.history.back();
      },
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
  }
  </style>
  