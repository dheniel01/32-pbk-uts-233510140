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
      <li
        v-for="(todo, index) in todos"
        :key="index"
        class="todo-item"
      >
        <label class="checkbox-label">
          <input
            type="checkbox"
            v-model="todo.done"
          />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
        </label>

        <button class="delete-button" @click="removeTodo(index)">
          Batalkan
        </button>
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

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f4f4f4;
  margin-bottom: 0.5rem;
  padding: 0.5rem;
  border-radius: 5px;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-grow: 1;
}

.done {
  text-decoration: line-through;
  color: gray;
}

.delete-button {
  background-color: #ff6b6b;
  border: none;
  padding: 0.3rem 0.8rem;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
</style>
