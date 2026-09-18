<script setup lang="ts">
import type { Todo } from '../types'

const props = defineProps<{
  todo: Todo
}>()

const emit = defineEmits<{
  toggle: [id: number]
  delete: [id: number]
}>()

function handleToggle() {
  emit('toggle', props.todo.id)
}

function handleDelete() {
  emit('delete', props.todo.id)
}


</script>

<template>
  <div>
    {{ todo.text }}
    <input :checked="todo.done" type="checkbox" @change="handleToggle"/>
    <button @click="handleDelete">Löschen</button>
  </div>
</template>

<style scoped>

</style>