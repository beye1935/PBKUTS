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

