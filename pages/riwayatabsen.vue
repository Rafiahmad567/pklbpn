<template>
  <div class="min-h-screen bg-gray-100">
    <div
      v-if="loading"
      class="d-flex justify-content-center align-items-center min-vh-100"
    >
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
    <div v-else>
      <!-- Header -->
      <div class="bg-gray-300 p-4 flex items-center gap-4">
        <NuxtLink to="/">
          <button class="btn btn-light">⬅ Back</button>
        </NuxtLink>
        <h1 class="text-2xl font-semibold">Riwayat Absensi</h1>
        <NuxtLink to="/absen" class="ms-auto">
          <button class="btn btn-primary">Isi Absen</button>
        </NuxtLink>
      </div>

      <!-- Tabel Riwayat -->
      <div class="p-4">
        <table class="table table-bordered">
          <thead>
            <tr class="bg-blue-200">
              <th class="p-2 text-left">Nama</th>
              <th class="p-2 text-left">Jurusan</th>
              <th class="p-2 text-left">Asal Sekolah</th>
              <th class="p-2 text-left">Status</th>
              <th class="p-2 text-left">Tanggal</th>
              <th class="p-2 text-left">Waktu Masuk</th>
              <th class="p-2 text-left">Waktu Keluar</th>
              <th class="p-2 text-left">Foto</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(absen, index) in riwayat"
              :key="index"
              :class="index % 2 === 0 ? 'bg-white' : 'bg-gray-200'"
            >
              <td class="p-2">{{ absen.nama?.nama || "-" }}</td>
              <td class="p-2">{{ absen.jurusan?.jurusan || "-" }}</td>
              <td class="p-2">{{ absen.asalsekolah?.asalsekolah || "-" }}</td>
              <td class="p-2">{{ absen.status?.nama || "-" }}</td>
              <!-- nama kecil -->
              <td class="p-2">{{ absen.tanggal || "-" }}</td>
              <td class="p-2">{{ absen.masuk || "-" }}</td>
              <td class="p-2">{{ absen.keluar || "-" }}</td>

              <td class="p-2">
                <a :href="absen.foto" target="_blank" v-if="absen.foto"
                  >Lihat Foto</a
                >
                <span v-else>-</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useSupabaseClient } from "#imports";

interface Absen {
  nama?: { nama: string };
  jurusan?: { jurusan: string };
  asalsekolah?: { asalsekolah: string };
  status?: { nama: string };
  tanggal: string;
  masuk?: string;
  keluar?: string;
  foto?: string;
}

const supabase = useSupabaseClient();
const riwayat = ref<Absen[]>([]);
const loading = ref(true);

const fetchRiwayat = async () => {
  try {
    const { data: absenData, error: absenError } = await supabase
      .from("absen")
      .select("*")
      .order("created_at", { ascending: false });

    if (absenError) {
      console.error("Supabase absen error:", absenError);
      throw absenError;
    }

    // Fetch related data
    const namaIds = absenData.map((item) => item.nama_id).filter(Boolean);
    const jurusanIds = absenData.map((item) => item.jurusan_id).filter(Boolean);
    const asalsekolahIds = absenData
      .map((item) => item.asalsekolah_id)
      .filter(Boolean);
    const statusIds = absenData.map((item) => item.status_id).filter(Boolean);

    const { data: namaData, error: namaError } = await supabase
      .from("nama")
      .select("id, nama")
      .in("id", namaIds);
    if (namaError) throw namaError;

    const { data: jurusanData, error: jurusanError } = await supabase
      .from("jurusan")
      .select("id, jurusan")
      .in("id", jurusanIds);
    if (jurusanError) throw jurusanError;

    const { data: asalsekolahData, error: asalsekolahError } = await supabase
      .from("asalsekolah")
      .select("id, asalsekolah")
      .in("id", asalsekolahIds);
    if (asalsekolahError) throw asalsekolahError;

    const { data: statusData, error: statusError } = await supabase
      .from("status")
      .select("id, nama")
      .in("id", statusIds);
    if (statusError) throw statusError;

    // Map data
    riwayat.value = absenData.map((absen) => ({
      ...absen,
      nama: namaData?.find((n) => n.id === absen.nama_id),
      jurusan: jurusanData?.find((j) => j.id === absen.jurusan_id),
      asalsekolah: asalsekolahData?.find((a) => a.id === absen.asalsekolah_id),
      status: statusData?.find((s) => s.id === absen.status_id),
    }));
  } catch (error) {
    console.error("Error fetching riwayat:", error);
    alert(`Error fetching data: ${(error as Error).message}`);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchRiwayat);
</script>

<style scoped>
table {
  width: 100%;
}
</style>
