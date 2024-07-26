<template>
  <form class="form">
    <input type="text" v-model="myQuery" placeholder="Agrega tu Tarea" />
    <button @click.prevent="handleClick">Guardar</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['setQuery'])

const myQuery = ref('')

const handleClick = () => {
  emit('setQuery', myQuery)
  myQuery.value = ''
}
</script>

<style scoped>
.form {
  display: flex;
  justify-content: center;
}
</style>
