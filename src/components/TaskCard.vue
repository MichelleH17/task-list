<template>
  <div class="flex max-w-sm m-auto bg-blue-50 p-4 w-full sm:w-sm my-12 rounded-xl shadow justify-between item">
    <p>{{ task.hoursToComplete }}h</p>
    <div>
      <p class="mb-2">{{ task.name }}</p>
      <p>{{ dateCreated }}</p>
    </div>
    <button @click="deleteTask" class="bg-blue-800 text-gray-50 px-2 py-1 rounded self-start">x</button>
  </div>
</template>

<script setup lang="ts">
import type { Task } from '../types'

const dateCreated = new Date().toLocaleDateString()

const props = defineProps<{
  task: Task
}>()

const emit = defineEmits<{
  (event: 'delete-task', id: number): void
}>()

const deleteTask = () => {
  emit('delete-task', props.task.id)
}
</script>
