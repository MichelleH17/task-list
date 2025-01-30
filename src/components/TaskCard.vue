<template>
  <div
    class="flex sm:max-w-sm m-auto bg-blue-50 p-4 w-full sm:w-sm my-12 rounded-xl shadow justify-between item"
  >
    <p>{{ task.hoursToComplete }}h</p>
    <div>
      <div>
        <p v-if="!isEditing" class="mb-2">{{ task.name }}</p>
        <input v-else type="text" v-model="editedTaskName" class="bg-white border border-gray-200 rounded-md p-1 mb-3" >
        <p>{{ dateCreated }}</p>
      </div>
    </div>
    <div v-if="!isEditing" class="flex gap-3">
      <button
        @click="startEditing"
        class="bg-blue-800 text-gray-50 px-2 py-1 rounded self-start"
      >
        Edit
      </button>
      <button @click="deleteTask" class="bg-red-800 text-gray-50 px-2 py-1 rounded self-start">
        x
      </button>
    </div>
      <button
        v-else
        @click="saveEdit"
        class="bg-green-500 text-gray-50 px-2 py-1 rounded self-start"
      >
        Save
      </button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { Task } from '../types'

const props = defineProps<{
  task: Task
}>()

const isEditing = ref(false)
const editedTaskName = ref(props.task.name)

const dateCreated = new Date().toLocaleDateString()

const emit = defineEmits<{
  (event: 'delete-task', id: number): void
  (event: 'update-task', task: Task): void
}>()

const deleteTask = () => {
  emit('delete-task', props.task.id)
}

const startEditing = () => {
  isEditing.value = true
}

const saveEdit = () => {
  if (editedTaskName.value.trim() !== '') {
    emit('update-task', { ...props.task, name: editedTaskName.value })
    isEditing.value = false
  }
}
</script>
