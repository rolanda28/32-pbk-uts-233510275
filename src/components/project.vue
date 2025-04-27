<template>
  <div class="container">
    <h1>📋 Daftar Kegiatan</h1>

    <div class="input-group">
      <input v-model="newActivity" @keyup.enter="addActivity" placeholder="Tambahkan kegiatan baru..." />
      <button @click="addActivity">Tambah</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showOnlyUnfinished" /> Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
        <input type="checkbox" v-model="activity.done" />
        <span :class="{ done: activity.done }">{{ activity.text }}</span>
        <button @click="removeActivity(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newActivity = ref('')
const activities = ref([])

const addActivity = () => {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ text: newActivity.value, done: false })
    newActivity.value = ''
  }
}

const removeActivity = (index) => {
  activities.value.splice(index, 1)
}

const showOnlyUnfinished = ref(false)

const filteredActivities = computed(() => {
  return showOnlyUnfinished.value
    ? activities.value.filter(activity => !activity.done)
    : activities.value
})
</script>