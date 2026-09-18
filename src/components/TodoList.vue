<script setup lang="ts">
import type { Todo } from '../types'

defineProps<{
  todos: Todo[]
}>()
</script>

<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.id }} | {{ todo.text }} | {{ todo.done }}
    </li>
  </ul>
</template>

<style scoped>

</style>