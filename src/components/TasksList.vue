<template>
  <section class="px-4">
    <div class="container-xl lg:container m-auto">
      <!-- <p v-if="lastTaskName" class="text-center text-green-500 mb-6">New task created: {{ lastTaskName }}</p> -->
      <span v-if="tasks.length === 0" class="flex justify-center">
        No tasks found
      </span>
      <div v-else class="flex flex-col text-center">
        <p class="text-center text-green-500 mb-6">New task created: {{ lastTaskName }}</p>
        <span class="text-3xl font-bold text-green-500 mb-6 ">
          Total tasks: {{ tasks.length }}
        </span>
      </div>
      <div class="mx-auto">
        <div v-if="tasks.length === 1" class="grid grid-cols-1 justify-center">
          <TaskCard :task="tasks[0]" @delete-task="deleteTask" @update-task="updateTask" />
        </div>
        <div v-else class="grid grid-cols-1 md:gap-3 lg:grid-cols-2 xl:grid-cols-3 justify-center">
          <TaskCard v-for="task in tasks" :key="task.id" :task="task" @delete-task="deleteTask" @update-task="updateTask" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import type { Task } from '../types'
import TaskCard from './TaskCard.vue'

defineProps<{
  tasks: Task[],
  lastTaskName: string
}>()

const emit = defineEmits<{
  (event: 'delete-task', id: number): void
  (event: 'update-task', task: Task): void
}>()

const deleteTask = (id: number) => {
  emit('delete-task', id)
}

const updateTask = (updatedTask: Task) => {
  emit('update-task', updatedTask)
}
</script>
