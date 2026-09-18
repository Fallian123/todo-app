<script setup lang="ts">
import { ref, computed } from 'vue'
import type { Todo } from '../types'
import TodoList from "./TodoList.vue";

const todos = ref<Todo[]>([])
const text = ref("")
const idCounter = ref(0)

type Filter = 'all' | 'open' | 'done'
const currentFilter = ref<Filter>('all')

const filteredTodos = computed(() => {
  if (currentFilter.value === 'open') {
    return todos.value.filter(todo => !todo.done)
  }
  if (currentFilter.value === 'done') {
    return todos.value.filter(todo => todo.done)
  }
  return todos.value
})

function addTodo() {
  if (text.value.trim() === "") {
    return
  }

  const newTodo = {
    id: idCounter.value,
    text: text.value,
    done: false
  }

  idCounter.value ++
  todos.value.push(newTodo)

  text.value = ""
}

function toggleTodo(id: number) {
  const found = todos.value.find(todo => todo.id === id)
  if (found) {
    found.done = !found.done
  }
}

function deleteTodo(id:number) {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

</script>

<template>
  <div>
    <h1>Meine Todos</h1>
    <input v-model="text" placeholder="Hier Aufgabe eintragen!" />
    <button @click="addTodo">Aufgabe hinzufügen</button>

    <div>
      <button @click="currentFilter = 'all'">Alle</button>
      <button @click="currentFilter = 'open'">Offen</button>
      <button @click="currentFilter = 'done'">Erledigt</button>
    </div>

    <TodoList :todos="filteredTodos" @toggle="toggleTodo" @delete="deleteTodo" />
  </div>
</template>

<style scoped>

</style>