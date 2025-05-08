// File: src/App.vue
<template>
  <div class="min-h-screen bg-yellow-100 text-center py-10 px-4 font-sans saitama-theme animate-fadeIn">
    <h1 class="text-4xl font-bold text-red-600 mb-6 shadow-md drop-shadow-lg">To-Do List Pahlawan🥊</h1>

    <div class="mb-4 flex justify-center items-center gap-2">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        class="task-input"
        placeholder="Masukkan misi rank C..."
      />
      <button @click="addTask" class="add-button hover:scale-105 transition-transform duration-200">
        Tambah Misi
      </button>
    </div>

    <div class="mb-6">
      <label class="text-sm text-gray-700">
        <input type="checkbox" v-model="showOnlyIncomplete" /> Tampilkan hanya misi yang belum selesai
      </label>
    </div>

    <ul class="max-w-xl mx-auto">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        class="task-item animate-slideIn"
      >
        <span
          :class="{
            'line-through text-gray-400 italic': task.completed,
            'text-black font-semibold': !task.completed
          }"
        >
          {{ task.text }}
        </span>
        <div class="flex gap-2">
          <button
            @click="toggleComplete(index)"
            class="complete-button hover:text-green-800 transition-colors duration-200"
          >
            {{ task.completed ? '↩ Batal' : '💥 One Punch!' }}
          </button>
          <button @click="deleteTask(index)" class="delete-button hover:text-red-800 transition-colors duration-200">
            ❌ Hapus
          </button>
        </div>
      </li>
    </ul>

    <footer class="mt-10 text-sm text-gray-800 font-medium bg-white/60 backdrop-blur-md p-2 rounded shadow">
      Rank Hero: <span class="text-red-600 font-bold">{{ heroRank }}</span> | Total Misi: {{ tasks.length }}
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const tasks = ref([])
const showOnlyIncomplete = ref(false)

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ text: newTask.value.trim(), completed: false })
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

const toggleComplete = (index) => {
  tasks.value[index].completed = !tasks.value[index].completed
}

const filteredTasks = computed(() => {
  return showOnlyIncomplete.value
    ? tasks.value.filter((task) => !task.completed)
    : tasks.value
})

const heroRank = computed(() => {
  const completed = tasks.value.filter(t => t.completed).length
  if (completed > 15) return 'S'
  if (completed > 10) return 'A'
  if (completed > 5) return 'B'
  return 'C'
})
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  background-color: #fff8dc;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-10px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes slideIn {
  from { opacity: 0; transform: translateX(-20px); }
  to { opacity: 1; transform: translateX(0); }
}

.animate-fadeIn {
  animation: fadeIn 0.8s ease-out;
}

.animate-slideIn {
  animation: slideIn 0.5s ease-out;
}

.saitama-theme {
  background-image: url('https://wallpapercave.com/wp/wp2389581.jpg');
  background-size: cover;
  background-position: center;
  background-blend-mode: lighten;
  min-height: 100vh;
}

.task-input {
  border: 2px solid #f87171;
  padding: 10px;
  width: 60%;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  font-size: 16px;
}

.add-button {
  background-color: #dc2626;
  color: white;
  padding: 10px 16px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  font-weight: bold;
  transition: all 0.2s ease-in-out;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 12px;
  margin-bottom: 10px;
  border-radius: 8px;
  transition: background-color 0.3s;
}

.task-item:hover {
  background-color: #fef3c7;
}

.complete-button {
  color: #16a34a;
  font-weight: 600;
  transition: all 0.2s;
}

.delete-button {
  color: #dc2626;
  font-weight: 600;
  transition: all 0.2s;
}
</style>