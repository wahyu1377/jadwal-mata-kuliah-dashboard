<script setup>
import { ref, onMounted } from 'vue'
import ScheduleForm from './components/ScheduleForm.vue'
import ScheduleList from './components/ScheduleList.vue'

const schedules = ref([])
const filterDay = ref('Semua') // Tambahkan state untuk filter

const days = ['Semua', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu']

// Load data
onMounted(() => {
  const saved = localStorage.getItem('classSchedules')
  if (saved) schedules.value = JSON.parse(saved)
})

const addSchedule = (newSchedule) => {
  schedules.value.push(newSchedule)
  saveToLocalStorage()
}

const deleteSchedule = (index) => {
  schedules.value.splice(index, 1)
  saveToLocalStorage()
}

const saveToLocalStorage = () => {
  localStorage.setItem('classSchedules', JSON.stringify(schedules.value))
}

// Fungsi untuk mendapatkan jadwal yang sudah difilter
const filteredSchedules = () => {
  if (filterDay.value === 'Semua') {
    return schedules.value
  }
  return schedules.value.filter(schedule => schedule.day === filterDay.value)
}
</script>

<template>
  <div class="app-container">
    <h1>Jadwal Kuliah</h1>
    <div class="filter-controls">
      <label>Filter Hari:</label>
      <select v-model="filterDay">
        <option v-for="day in days" :key="day" :value="day">{{ day }}</option>
      </select>
    </div>
    <div class="content-wrapper">
      <ScheduleForm @add-schedule="addSchedule" />
      <ScheduleList 
        :schedules="filteredSchedules()" 
        @delete-schedule="deleteSchedule" 
      />
    </div>
  </div>
</template>

<style scoped>
.filter-controls {
  margin-bottom: 1.5rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.filter-controls label {
  font-weight: 500;
}

.filter-controls select {
  padding: 0.5rem;
  border-radius: 4px;
  border: 1px solid #ddd;
}
</style>