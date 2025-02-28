<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li 
        v-for="(choice, index) in randomChoice"
        :key="choice"
        >
        <Answer 
          :disabled="hasAnswer"
          :id="`answer${index}`"
          :value="choice"
          @change="onAnswer"
          v-model="answer"
          :correctaAnswer="question.correct_answer"
        />
      </li>
    </ul>
  </div>
</template>

<script setup>
import { shuffleArray } from '@/functions/array';
import { computed, onMounted, onUnmounted, ref } from 'vue';
import Answer from './Answer.vue';

const props = defineProps({
  question: Object
})
const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)
const randomChoice = computed(() => shuffleArray(props.question.choices))
let timer

const onAnswer = () => {
  clearTimeout(timer)
  timer = setTimeout(() => {
    emits('answer', answer.value)
  }, 1_500)
}

onMounted(() => {
  timer = setTimeout(() => {
    answer.value = ''
    onAnswer()
  }, 3_000)
})

onUnmounted(() => {
  clearTimeout(timer)
})

</script>

<style>
.question{
  padding-top: 2rem;
}

.question button{
  margin-left: auto;
  display: block;
}
.question li{
  list-style: none;
}
</style>