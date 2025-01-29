<template>
  <section class="px-4">
    <div class="container-xl lg:container m-auto">
      <span v-if="tasks.length === 0" class="flex justify-center">
        No tasks found
      </span>
      <span v-else class="text-3xl font-bold text-green-500 mb-6 flex justify-center">
        Total tasks: {{ tasks.length }}
      </span>
      <div class="grid grid-cols-1 gap-3 md:grid-cols-2 lg:grid-cols-3 justify-center">
        <TaskCard v-for="task in tasks" :key="task.id" :task="task" @delete-task="deleteTask" />
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import type { Task } from '../types'
import TaskCard from './TaskCard.vue'

defineProps<{
  tasks: Task[]
}>()

const emit = defineEmits<{
  (event: 'delete-task', id: number): void
}>()

const deleteTask = (id: number) => {
  emit('delete-task', id)
}
</script>
