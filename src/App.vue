<template>
  <div>
    <form @submit.prevent="addTodo">
      <input
        v-model="newTodo"
        placeholder="Tambahkan kegiatan"
        class="todo-input"
      />
    </form>

    <ul v-if="todos.length" class="todo-list">
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
      </li>
    </ul>
    <p v-else>Belum ada kegiatan.</p>
  </div>
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
.todo-input {
  padding: 0.5rem;
  width: 70%;
  margin-right: 0.5rem;
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
