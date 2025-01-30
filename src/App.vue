<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import TasksList from './components/TasksList.vue'
import { ref } from 'vue';
import type { Task } from './types';

const tasks = ref<Task[]>([])
const lastTaskName = ref<string>('')

const addTask = (task: Task) => {
  tasks.value.push(task)
  lastTaskName.value = task.name
}

const deleteTask = (id: number) => {
  tasks.value = tasks.value.filter(task => task.id !== id)
}
</script>

<template>
  <main>
    <TaskForm :tasks="tasks" @add-task="addTask" />
    <TasksList :tasks="tasks" @delete-task="deleteTask" :last-task-name="lastTaskName" />
  </main>
</template>
