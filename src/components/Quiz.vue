<template>
  <div>
    <h1>{{ quiz.title }}</h1>
    <Progress :value="step" :max="quiz.questions.length - 1"/>
    <Question :question="question" />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';

const props = defineProps({
  quiz: Object
})

const step = ref(0)

const question = computed(() => props.quiz.questions[step.value])
</script>