<template>
  <div>
    <h1>{{ quiz.title }}</h1>
    <Progress :value="step" :max="quiz.questions.length - 1"/>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Progress from './Progress.vue';

defineProps({
  quiz: Object
})

const step = ref(0)
</script>