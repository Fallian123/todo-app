<script setup lang="ts">
import { ref } from 'vue'
import type { Todo } from '../types'
import TodoList from "./TodoList.vue";

const todos = ref<Todo[]>([])
const text = ref("")
const idCounter = ref(0)

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
</script>

<template>
  <div>
    <h1>Meine Todos</h1>
    <input v-model="text" placeholder="Hier Aufgabe eintragen!" />
    <button @click="addTodo">Aufgabe hinzufügen</button>
    <TodoList :todos="todos"></TodoList>
  </div>
</template>

<style scoped>

</style>