<template>
  <div>
    <h1>{{ quiz.title }}</h1>
  </div>
</template>

<script setup>
defineProps({
  quiz: Object
})
</script>