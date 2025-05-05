<template>
  <main class="container">
    <h1>Daftar Kegiatan</h1>

    <form @submit.prevent="addTodo">
      <input
        v-model="newTodo"
        placeholder="Tambahkan kegiatan"
        class="todo-input"
      />
      <button type="submit">Tambah</button>
    </form>

    <ul v-if="todos.length" class="todo-list">
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
      </li>
    </ul>
    <p v-else>Belum ada kegiatan.</p>
  </main>
</template>

<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const todos = ref([])

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push(newTodo.value.trim())
    newTodo.value = ''
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: sans-serif;
}

form {
  margin-bottom: 1rem;
}

.todo-input {
  padding: 0.5rem;
  width: 70%;
  margin-right: 0.5rem;
}

button {
  padding: 0.5rem 1rem;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin-top: 1rem;
}

.todo-list li {
  background: #f4f4f4;
  margin-bottom: 0.5rem;
  padding: 0.5rem;
  border-radius: 5px;
}
</style>
