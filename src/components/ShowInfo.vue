<template>
  <table>
    <thead>
      <tr>
        <th>Tarea</th>
        <th>Estado</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="task in props.arrTasks" :key="task.name">
        <td>
          <router-link :to="{ name: 'task', params: { name: task.name } }">{{
            task.name
          }}</router-link>
        </td>
        <td class="status" @click="handleStatus(task.name)">{{ task.status }}</td>
        <td>
          <div class="edit" @click="editT(task)">editar</div>
          <div class="delete" @click="deleteT(task.name)">Borrar</div>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
const props = defineProps(['arrTasks'])
const emit = defineEmits(['changeStatus', 'deleteTask', 'editTask'])

const handleStatus = (name) => {
  emit('changeStatus', name)
}

const deleteT = (name) => {
  emit('deleteTask', name)
}

const editT = (name) => {
  emit('editTask', name)
}
</script>

<style>
.status {
  cursor: pointer;
}
.delete {
  cursor: pointer;
}
.edit {
  cursor: pointer;
}
</style>
