<script setup lang="ts">
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue'
import TasksList from './components/TasksList.vue'
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

const updateTask = (updatedTask: Task) => {
  const task = tasks.value.find(task => task.id === updatedTask.id)
  if (task) {
    task.name = updatedTask.name
    task.hoursToComplete = updatedTask.hoursToComplete
  }
}
</script>

<template>
  <main>
    <TaskForm :tasks="tasks" @add-task="addTask" />
    <TasksList :tasks="tasks" @delete-task="deleteTask"
    @update-task="updateTask"
    :last-task-name="lastTaskName" />
  </main>
</template>
