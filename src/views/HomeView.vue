<script setup>
import InputTask from '@/components/InputTask.vue'
import ShowInfo from '@/components/ShowInfo.vue'
import { ref } from 'vue'

const status = ref(['Pendiente', 'Terminada'])
const editing = ref(false)
const query = ref('')
const newQuery = ref('')

const addTask = (q) => {
  const newTask = {
    name: q.value,
    status: status.value[0]
  }

  arrTasks.value = [...arrTasks.value, newTask]

  saveToLocal()
}

const saveEditTask = () => {
  console.log(query.value)
  editing.value = false
}

const arrTasks = ref(JSON.parse(localStorage.getItem('tasks')) || [])

const changeStatus = (n) => {
  arrTasks.value.forEach((task) => {
    if (task.name === n) task.status = status.value[1]
  })
}

const deleteTask = (n) => {
  const temp = arrTasks.value.filter((task) => task.name !== n)
  arrTasks.value = [...temp]
  saveToLocal()
}

const editTask = (n) => {
  console.log(n)
  editing.value = true
  newQuery.value = n.name
}

const saveToLocal = () => {
  localStorage.setItem('tasks', JSON.stringify(arrTasks.value))
}
</script>

<template>
  <main>
    <h1>Todo App</h1>
    <InputTask @setQuery="addTask" />
    <ShowInfo
      :arrTasks="arrTasks"
      @changeStatus="changeStatus"
      @deleteTask="deleteTask"
      @editTask="editTask"
    />

    <form v-if="editing">
      <input type="text" v-model="newQuery" placeholder="Agrega tu Tarea" />
      <button @click.prevent="saveEditTask">Editar</button>
    </form>
  </main>
</template>

<style>
h1 {
  text-align: center;
  margin: auto;
}
</style>
