<template>
  <div class="h-full text-white flex items-center justify-center px-4">
    <div
      class="w-full max-w-3xl ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30 rounded-lg p-6"
    >
      <h2 class="text-3xl font-bold text-center mb-6">Detail Ujian</h2>

      <form class="space-y-4" @submit.prevent="handleSubmit">
        <!-- Judul ujiannya -->
        <div>
          <label class="block mb-1">Judul</label>
          <UInput
            v-model="formData.judul"
            :ui="{
              base: 'w-full p-2 rounded-md ring ring-primary-light/50 bg-primary-dark focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            type="text"
            class="w-full"
            size="xl"
            placeholder="Masukkan judul ujian"
          />
        </div>

        <!-- Deskripsi nya-->
        <div>
          <label class="block mb-1">Deskripsi</label>
          <UTextarea
            v-model="formData.deskripsi"
            :rows="3"
            :ui="{
              base: 'w-full p-2 rounded-md ring ring-primary-light/50 bg-primary-dark focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            class="w-full"
            placeholder="Masukkan deskripsi..."
          ></UTextarea>
        </div>

        <!-- Durasi Menit -->
        <div>
          <label class="block mb-1">Durasi (menit)</label>
          <UInputNumber
            v-model="formData.durasi_menit"
            :ui="{
              base: 'w-full p-2 rounded-md ring ring-primary-light/50 bg-primary-dark focus-visible:ring-primary-light ',
            }"
            :min="1"
            :max="120"
            color="primary"
            :increment="{
              color: 'neutral',
            }"
            :decrement="{
              color: 'neutral',
            }"
            placeholder="Misal: 90"
            class="w-full"
          />
        </div>

        <!-- Tanggal Mulai & Tanggal Selesai harusnyaa -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label class="block mb-1">Tanggal Mulai</label>
            <UInput
              v-model="formData.tanggal_mulai"
              :ui="{
                base: 'w-full p-2 rounded-md ring ring-primary-light/50 bg-primary-dark focus-visible:ring-primary-light',
              }"
              size="xl"
              type="date"
              class="w-full"
            />
          </div>
          <div>
            <label class="block mb-1">Tanggal Selesai</label>
            <UInput
              v-model="formData.tanggal_selesai"
              :ui="{
                base: 'w-full p-2 rounded-md ring ring-primary-light/50 bg-primary-dark focus-visible:ring-primary-light ',
              }"
              size="xl"
              type="date"
              class="w-full"
            />
          </div>
        </div>

        <!-- Jam mulai -->
        <div>
          <label class="block mb-1">Jam Mulai</label>
          <UInput
            v-model="formData.jam_mulai"
            :ui="{
              base: 'w-full p-2 bg-primary-dark rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            type="time"
            size="xl"
            class="w-full"
          />
        </div>

        <div>
          <label class="block mb-1">Batas Percobaan</label>
          <UInputNumber
            v-model="formData.batas_percobaan"
            :ui="{
              base: 'w-full bg-primary-dark p-2 rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            :increment="{
              color: 'neutral',
            }"
            :decrement="{
              color: 'neutral',
            }"
            size="xl"
            class="w-full"
          />
        </div>

        <!-- password tes atau uian -->
        <div>
          <label class="block mb-1">Password Tes</label>
          <UInput
            v-model="formData.password_tes"
            :ui="{
              base: 'w-full bg-primary-dark p-2 rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            type="text"
            size="xl"
            class="w-full"
          />
        </div>

        <!-- MapelUjian -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label class="block mb-1">Mapel</label>
            <UInput
              v-model="formData.mapel"
              :ui="{
                base: 'w-full bg-primary-dark p-2 rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
              }"
              type="text"
              size="xl"
              class="w-full"
            />
          </div>
          <div>
            <label class="block mb-1">Jenis Ujian</label>
            <USelect
              v-model="formData.jenis_ujian"
              :ui="{
                base: 'bg-primary-dark ring-primary-light/50 w-full p-2',
              }"
              variant="outline"
              size="xl"
              :items="jenisUjian"
              placeholder="Pilih jenis ujian"
            />
          </div>
        </div>

        <!-- Semester berapa gitu -->
        <div>
          <label class="block mb-1">Semester</label>
          <UInput
            v-model="formData.semester"
            :ui="{
              base: 'w-full p-2 bg-primary-dark rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
            }"
            class="w-full"
            :increment="{
              color: 'neutral',
            }"
            :decrement="{
              color: 'neutral',
            }"
            :min="1"
            size="xl"
          />
        </div>

        <!-- Kelas-->
        <div>
          <label class="block mb-1">Kelas</label>
          <div class="space-y-2">
            <UInput
              v-model="formData.kelas[0]"
              type="text"
              :ui="{
                base: 'w-full bg-primary-dark p-2 rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
              }"
              size="xl"
              class="w-full"
              placeholder="Kelas 1 (misal: XI-RPL-2)"
            />
            <UInput
              v-model="formData.kelas[1]"
              type="text"
              :ui="{
                base: 'w-full bg-primary-dark p-2 rounded-md ring ring-primary-light/50 focus-visible:ring-primary-light placeholder:text-primary-light/30',
              }"
              size="xl"
              class="w-full"
              placeholder="Kelas 2 (misal: XI-RPL-2)"
            />
          </div>
        </div>

        <!-- Tombol bol tombol -->
        <div class="pt-4">
          <button
            type="submit"
            class="w-full hover:ring-primary-light cursor-pointer ring ring-primary-light/50 py-2 rounded-md text-white"
          >
            Buat Ujian
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts" setup>
definePageMeta({
  layout: "admin",
  middleware: "auth",
  path: "/admin/ujian/tambah",
});

const { CreateTest } = useTest();

const jenisUjian = ["PAS", "PAT"];

const formData = ref({
  tes_id: "",
  judul: "",
  deskripsi: "",
  durasi_menit: 0,
  tanggal_mulai: "",
  tanggal_selesai: "",
  batas_percobaan: 0,
  password_tes: "",
  mapel: "",
  jenis_ujian: "",
  semester: 0,
  kelas: ["", ""],
  jam_mulai: "",
});

const handleSubmit = async () => {
  try {
    const response = await CreateTest({
      ... formData.value,
      semester: formData.value.semester.toString()
    })
    console.log("berhasil", response);
    navigateTo("/admin/ujian");
  } catch (error) {
    console.error("Gagal membuat tes:", error);
  }
};
</script>

<style></style>
