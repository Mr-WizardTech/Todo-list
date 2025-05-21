<template>
  <div class="p-4">
    <h1 class="text-xl font-bold mb-4">ToDo List</h1>

    <!-- Form to add task -->
    <form @submit.prevent="addTask" class="mb-4 space-y-2">
      <input v-model="taskName" placeholder="Task Name" class="border p-2 w-full" />
      <input v-model="description" placeholder="Description" class="border p-2 w-full" />
      <input type="date" v-model="date" class="border p-2 w-full" />
      <select v-model="status" class="border p-2 w-full">
        <option value="Pending">Pending</option>
        <option value="Completed">Completed</option>
      </select>
      <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">Add Task</button>
    </form>

    <!-- Table -->
    <table class="w-full border">
      <thead>
        <tr class="bg-gray-100">
          <th class="border p-2">Date</th>
          <th class="border p-2">Task Name</th>
          <th class="border p-2">Description</th>
          <th class="border p-2">Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td class="border p-2">{{ formatDate(task.date) }}</td>
          <td class="border p-2">{{ task.name }}</td>
          <td class="border p-2">{{ task.description }}</td>
          <td class="border p-2">{{ task.status }}</td>
        </tr>

      
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'


const tasks = ref([])
const taskName = ref('')
const description = ref('')
const date = ref('')
const status = ref('Pending')

const addTask = () => {
  if (!taskName.value || !description.value || !date.value) return

  tasks.value.push({
    name: taskName.value,
    description: description.value,
    date: date.value,
    status: status.value
  })

  taskName.value = ''
  description.value = ''
  date.value = ''
  status.value = 'Pending'
}

const formatDate = (dateStr) => {
  const options = { day: '2-digit', month: 'short', year: 'numeric' }
  return new Date(dateStr).toLocaleDateString('en-GB', options).replace(/ /g, '-')
}
</script>
