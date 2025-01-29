<template>
  <section class="bg-gray-100 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Add Task</h2>
      <p class="text-center">Enter the task name</p>
      <form @submit.prevent="addTask" class="flex flex-col gap-4 max-w-sm m-auto">
        <label for="newTask">
          Task Name
        </label>
        <input type="text" id="newTask" name="newTask" v-model="newTask" />
        <label for="hoursToComplete">
          Hours to complete
        </label>
        <input type="number" id="hoursToComplete" name="hoursToComplete" v-model="hoursToComplete" min="1" />
        <button type="submit" class="bg-green-500 px-5 py-2 rounded-3xl text-gray-50 hover:bg-green-600">
          Add Task
        </button>
      </form>
    </div>
  </section>
  <TasksList :tasks="tasks" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { Task } from '../types'
import TasksList from './TasksList.vue'

const newTask = ref('')
const tasks = ref<Task[]>([])
const hoursToComplete = ref(1)

const addTask = () => {
  if (newTask.value.trim() !== '') {
    const task: Task = {
      id: tasks.value.length + 1,
      name: newTask.value,
      hoursToComplete: hoursToComplete.value
    }
    tasks.value.push(task)
    newTask.value = ''
    hoursToComplete.value = 1
  }
}

</script>
