<template>
  <h1>Recap</h1>
  <p>
    {{ hasWon ? quiz.success_message : quiz.failure_message }}
  </p>
  <p>
    Score : {{ score }}/{{ quiz.questions.length }}
  </p>
  <button @click="onLoad">Rejouer</button>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  answers: Array,
  quiz: Object
})

const score = computed(() => {
  return props.quiz.questions.reduce((acc, question, k) => {
    if (question.correct_answer === props.answers[k]) {
      return acc + 1
    }
    return acc
  }, 0)
})

const hasWon = computed(() => score.value >= props.quiz.minimum_score)
const onLoad = () => {
  location.reload()
}
</script>

<style>
button{
  margin-left: auto;
  display: block;
}
</style>