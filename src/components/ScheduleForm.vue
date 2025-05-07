<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-schedule'])

const form = ref({
  courseName: '',
  day: 'Senin',
  startTime: '',
  endTime: '',
  credits: 2,
  className: '',
  room: '',
  building: '',
  lecturer: '',
  type: 'Teori',
  day: 'senin'
})

const days = ['Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu']

const submitForm = () => {
  if (!form.value.courseName || !form.value.startTime || !form.value.endTime) {
    alert('Harap isi nama matakuliah, jam mulai, dan jam selesai')
    return
  }
  
  emit('add-schedule', { ...form.value })
  
  // Reset form setelah submit
  form.value = {
    courseName: '',
    day: 'Senin',
    startTime: '',
    endTime: '',
    credits: 2,
    className: '',
    room: '',
    building: '',
    lecturer: '',
    type: 'Teori'
  }
}
</script>

<template>
  <div class="form-container">
    <h2>Tambah Jadwal Baru</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label>Nama Mata Kuliah:</label>
        <input type="text" v-model="form.courseName" required>
      </div>
      
      <div class="form-row">
        <div class="form-group">
          <label>Hari:</label>
          <select v-model="form.day">
            <option v-for="day in days" :key="day" :value="day">{{ day }}</option>
          </select>
        </div>
        
        <div class="form-group">
          <label>Jam Mulai:</label>
          <input type="time" v-model="form.startTime" required>
        </div>
        
        <div class="form-group">
          <label>Jam Selesai:</label>
          <input type="time" v-model="form.endTime" required>
        </div>
      </div>
      
      <div class="form-row">
        <div class="form-group">
          <label>Jumlah SKS:</label>
          <input type="number" v-model="form.credits" min="1" max="6">
        </div>
        
        <div class="form-group">
          <label>Kelas:</label>
          <input type="text" v-model="form.className">
        </div>
      </div>
      
      <div class="form-row">
        <div class="form-group">
          <label>Ruangan:</label>
          <input type="text" v-model="form.room">
        </div>
        
        <div class="form-group">
          <label>Gedung:</label>
          <input type="text" v-model="form.building">
        </div>
      </div>
      
      <div class="form-group">
        <label>Dosen Pengajar:</label>
        <input type="text" v-model="form.lecturer">
      </div>
      
      <div class="form-group">
        <label>Jenis Mata Kuliah:</label>
        <div class="radio-group">
          <label>
            <input type="radio" v-model="form.type" value="Teori"> Teori
          </label>
          <label>
            <input type="radio" v-model="form.type" value="Praktikum"> Praktikum
          </label>
        </div>
      </div>
      
      <button type="submit" class="submit-btn">Simpan Jadwal</button>
    </form>
  </div>
</template>