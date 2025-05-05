<template>
  <div class="container">
    <h1>Daftar Kegiatan</h1>

    <form @submit.prevent="addTask">
      <input v-model="newTask" placeholder="Tambah kegiatan..." />
      <button type="submit">Tambah</button>
    </form>

    <div>
      <label>
        <input type="checkbox" v-model="showOnlyUnfinished" />
        Tampilkan hanya kegiatan belum selesai
      </label>
    </div>

    <ul>
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="{ done: task.done }"
      >
        <input type="checkbox" v-model="task.done" />
        <span>{{ task.text }}</span>
        <button @click="removeTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const showOnlyUnfinished = ref(false)
const tasks = ref([])

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, done: false })
    newTask.value = ''
  }
}

const removeTask = (index) => {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() => {
  return showOnlyUnfinished.value
    ? tasks.value.filter(task => !task.done)
    : tasks.value
})
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: auto;
  padding: 20px;
}

.done span {
  text-decoration: line-through;
  color: gray;
}
</style>