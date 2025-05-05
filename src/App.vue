<template>
  <main class="container">
    <h1>📝 Daftar Kegiatan</h1>

    <form @submit.prevent="addTodo" class="form">
      <input
        v-model="newTodo"
        placeholder="Tambahkan kegiatan"
        class="todo-input"
      />
      <button type="submit" class="add-button">
        ➕ Tambah
      </button>
    </form>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul v-if="filteredTodos.length" class="todo-list">
      <li
        v-for="(todo, index) in filteredTodos"
        :key="index"
        class="todo-item"
      >
        <label class="checkbox-label">
          <input
            type="checkbox"
            v-model="todo.done"
          />
          <span :class="{ done: todo.done }">
            {{ todo.text }}
          </span>
        </label>

        <button class="delete-button" @click="removeTodo(index)" title="Batalkan">
          🗑️
        </button>
      </li>
    </ul>
    <p v-else class="no-data">Tidak ada kegiatan ditampilkan.</p>
  </main>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const todos = ref([])
const showOnlyIncomplete = ref(false)

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({
      text: newTodo.value.trim(),
      done: false
    })
    newTodo.value = ''
  }
}

function removeTodo(index) {
  todos.value.splice(index, 1)
}

const filteredTodos = computed(() => {
  return showOnlyIncomplete.value
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})
</script>

<style scoped>
:root {
  --primary-color: #42b883;
  --danger-color: #ff6b6b;
  --background: #e0f7fa; /* Mengubah latar belakang menjadi biru muda */
  --item-bg: #ffffff;
  --text-color: #2c3e50;
}


body {
  background: var(--background);
  margin: 0;
  padding: 0;
}

.container {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: 'Segoe UI', sans-serif;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: var(--text-color);
  margin-bottom: 1rem;
}

.form {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.todo-input {
  flex: 1;
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 1rem;
}

.add-button {
  background-color: var(--primary-color);
  color: white;
  border: none;
  border-radius: 6px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-button:hover {
  background-color: #369f75;
}

.filter {
  margin-bottom: 1rem;
  font-size: 0.95rem;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--item-bg);
  margin-bottom: 0.5rem;
  padding: 0.75rem 1rem;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  transition: transform 0.2s ease;
}

.todo-item:hover {
  transform: translateY(-2px);
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  flex-grow: 1;
  font-size: 1rem;
}

.done {
  text-decoration: line-through;
  color: gray;
}

.delete-button {
  background-color: transparent;
  border: none;
  color: var(--danger-color);
  font-size: 1.2rem;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.delete-button:hover {
  transform: scale(1.2);
}

.no-data {
  text-align: center;
  color: #888;
  font-style: italic;
}
</style>

