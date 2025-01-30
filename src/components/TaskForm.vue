<template>
  <section class="bg-gray-100 px-4 py-10 md:max-w-md md:mx-auto mx-4 my-12 rounded-xl shadow">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-3 text-center">Add Task</h2>
      <p class="text-center mb-6">Enter the task name</p>
      <form @submit.prevent="addTask" class="flex flex-col gap-1 max-w-sm m-auto">
        <label for="newTask" class="font-semibold"> Task Name </label>
        <input
          type="text"
          id="newTask"
          name="newTask"
          v-model="newTask"
          class="bg-white border border-gray-200 rounded-md p-1 mb-3"
        />
        <label for="hoursToComplete" class="font-semibold"> Hours to complete </label>
        <input
          type="number"
          id="hoursToComplete"
          name="hoursToComplete"
          v-model="hoursToComplete"
          :min="1"
          class="bg-white border border-gray-200 rounded-md p-1 mb-6"
        />
        <button
          type="submit"
          class="bg-green-500 px-5 py-2 rounded-xl text-gray-50 hover:bg-green-600 font-semibold"
        >
          Add Task
        </button>
      </form>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { Task } from '../types'

const props = defineProps<{
  tasks: Task[]
}>()

const emit = defineEmits<{
  (event: 'add-task', task: Task): void
}>()

const newTask = ref('')
const hoursToComplete = ref(1)

const addTask = () => {
  if (newTask.value.trim() !== '') {
    const task: Task = {
      id: props.tasks.length + 1,
      name: newTask.value,
      hoursToComplete: hoursToComplete.value,
    }
    emit('add-task', task)
    newTask.value = ''
    hoursToComplete.value = 1
  }
}
</script>
