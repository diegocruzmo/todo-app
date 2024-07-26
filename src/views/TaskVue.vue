<template>
  <div>{{ route.params.name }}</div>
</template>

<script setup>
import { useRoute } from 'vue-router'

const route = useRoute()
</script>

<style></style>
