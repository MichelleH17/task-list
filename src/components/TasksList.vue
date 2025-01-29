<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Total task: {{ tasks.length }}
      </h2>
      <div class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <TaskCard v-for="task in tasks" :key="task.id" :task="task" />
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
</script>
