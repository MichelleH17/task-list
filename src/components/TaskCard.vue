<template>
  <div class="flex gap-4 max-w-sm m-auto bg-blue-50 py-10 w-full sm:w-sm my-12 rounded-xl shadow">
    <p>{{ task.hoursToComplete }}h</p>
    <p>{{ task.name }}</p>
    <button @click="deleteTask" class="bg-blue-800 text-gray-50 px-2 p-0-5 rounded">x</button>
  </div>
</template>

<script setup lang="ts">
import type { Task } from '../types'

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
