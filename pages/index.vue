<template>
  <div class="position-relative min-vh-100 d-flex align-items-center justify-content-center bg-light">

    <!-- Background image/logo -->
    <div class="position-absolute top-0 start-0 w-100 h-100 bg-logo"></div>

    <!-- Tombol Login -->
    <NuxtLink to="/login"><button class="btn btn-light position-absolute top-0 end-0 m-3 fw-bold">Login</button></NuxtLink>

    <!-- Card Form -->
    <div class="glass-card p-4 rounded-4 shadow-lg" style="width: 100%; max-width: 400px; z-index: 10;">
      <form @submit.prevent="kirimData">
        
        <div class="mb-3">
          <select v-model="form.nama" class="form-control form-control-lg form-select rounded-5 mb-2 abu">
            <option value="">Nama</option>
           <option v-for="(item, i) in members" :key="i" :value="item.id">{{ item.nama }}</option>
          </select>
        </div>

        <div class="mb-3">
          <select v-model="form.jurusan" class="form-control form-control-lg form-select rounded-5 mb-2 abu">
            <option value="">jurusan</option>
           <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.jurusan }}</option>
          </select>
        </div>

        <div class="mb-3">
          <select v-model="form.asalsekolah" class="form-control form-control-lg form-select rounded-5 mb-2 abu">
            <option value="">asal sekolah</option>
           <option v-for="(item, i) in opas" :key="i" :value="item.id">{{ item.asalsekolah }}</option>
          </select>
        </div>

        <div class="mb-3">
          <select v-model="form.status" class="form-control form-control-lg form-select rounded-5 mb-2 abu">
            <option value="">status</option>
           <option v-for="(item, i) in rians" :key="i" :value="item.id">{{ item.Nama }}</option>
          </select>
        </div>

        <!-- Upload Foto -->
        <div class="text-center mb-3">
             <label>Upload Foto Produk</label>
             <input @change="handleFileInput" type="file" class="form-control form-control-lg radius" id="file-input" accept="image/*" placeholder="Upload Foto Produk:" required />
          </div>

        <div class="text-center">
          <button type="submit" class="btn btn-dark px-4 fw-bold text-white">kirim</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref([]);
const objectives = ref([]);
const opas= ref([]);
const rians= ref([]);
const form = ref({
    jurusan: "",
    asalsekolah: "",
    status: "",
    photo: "",
    nama: "",
});
const handleFileInput = (event) => {
  file.value = event.target.files[0];
};
const kirimData = async () => {
    console.log(form.value)
    const { error } = await supabase.from("absen").insert([form.value])
    if(!error) navigateTo("/andaberhasil")
    else throw error
    if (!file.value)
    alert("Pilih file terlebih dahulu!");
    return;
}
try {
    const { data, error } = await supabase.storage.from("foto").upload(`public/${file.value.name}`, file.value);

    if (error) {
      throw error;
    }

    const publicUrl = supabase.storage.from("foto").getPublicUrl(`public/${file.value.name}`).data.publicUrl;
    const { error: insertError } = await supabase.from("absen").insert([{ foto: publicUrl, ...form.value }]);

    if (!error) {
      window.location.reload();
    }

    if (insertError) {
      throw insertError;
    }

    alert("berhasil dikirim!");
  } catch (error) {
    console.error("Error uploading file:", error.message);
    // alert("Gagal mengupload file.");
  }

const getnama = async () => {
    const { data, error } = await supabase.from("nama").select("*")
    if(data) members.value = data
};

const getjurusan = async () => {
    const { data, error } = await supabase.from("jurusan").select("*")
    if(data) objectives.value = data
};
const getasalsekolah= async () => {
    const { data, error } = await supabase.from("asalsekolah").select("*")
    if(data) opas.value = data
};
const getstatus= async () => {
    const { data, error } = await supabase.from("status").select("*")
    if(data) rians.value = data
};
onMounted(() => {
    getnama();
    getjurusan();
    getasalsekolah();
    getstatus();
});
</script>

<style scoped>
.bg-logo {
  background: url('/assets/logo_pbn.png') no-repeat center center;
  background-size: contain;
  opacity: 0.1;
  z-index: 1;
  pointer-events: none; /* Tambahkan ini */
}


.glass-card {
  backdrop-filter: blur(10px);
  background-color: rgba(255, 255, 255, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.3);
}
</style>
