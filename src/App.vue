<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import TasksList from './components/TasksList.vue'
import { ref } from 'vue';
import type { Task } from './types';

const tasks = ref<Task[]>([])

const addTask = (task: Task) => {
  tasks.value.push(task)
}
</script>

<template>
  <main>
    <TaskForm :tasks="tasks" @add-task="addTask" />
    <TasksList :tasks="tasks" />
  </main>
</template>
