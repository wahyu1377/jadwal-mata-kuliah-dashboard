
<script setup>

defineProps({
  schedules: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['delete-schedule'])
</script>

<template>
  <div class="list-container">
    <h2>Daftar Jadwal Kuliah</h2>
    
    <div v-if="schedules.length === 0" class="empty-message">
      Belum ada jadwal yang ditambahkan
    </div>
    
    <div v-else>
      <div v-for="(schedule, index) in schedules" :key="index" class="schedule-card">
        <div class="schedule-header">
          <h3>{{ schedule.courseName }}</h3>
          <span class="credits">{{ schedule.credits }} SKS</span>
          <span class="type-badge" :class="{ 'theory': schedule.type === 'Teori', 'practice': schedule.type === 'Praktikum' }">
            {{ schedule.type }}
          </span>
        </div>
        
        <div class="schedule-details">
          <p><strong>Hari:</strong> {{ schedule.day }}</p>
          <p><strong>Jam:</strong> {{ schedule.startTime }} - {{ schedule.endTime }}</p>
          <p><strong>Kelas:</strong> {{ schedule.className }}</p>
          <p><strong>Lokasi:</strong> Gedung {{ schedule.building }}, Ruang {{ schedule.room }}</p>
          <p><strong>Dosen:</strong> {{ schedule.lecturer }}</p>
        </div>
        
        <button @click="emit('delete-schedule', index)" class="delete-btn">
          Hapus
        </button>
      </div>
    </div>
  </div>
</template>