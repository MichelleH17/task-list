<template>
  <div>
    {{ task.name }} - {{ task.hoursToComplete }} hours
  </div>
</template>

<script setup lang="ts">
import type { Task } from '../types'

defineProps<{
  task: Task
}>()
</script>
