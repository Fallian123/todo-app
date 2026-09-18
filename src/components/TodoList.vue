<script setup lang="ts">
import type { Todo } from '../types'
import TodoItem from "./TodoItem.vue";

defineProps<{
  todos: Todo[]
}>()

const emit = defineEmits<{
  toggle: [id: number]
  delete: [id: number]
}>()

</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <TodoItem :todo="todo" @toggle="emit('toggle', $event)" @delete="emit('delete', $event)"/>
    </li>
  </ul>
</template>

<style scoped>

</style>