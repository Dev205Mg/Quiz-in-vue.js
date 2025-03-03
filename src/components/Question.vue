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
  <p>
    Temps restant : {{ t }} s
  </p>
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
const timeInResponse = 10000
let time
let t = ref(timeInResponse / 1000)

const onAnswer = () => {
  clearTimeout(timer)
  timer = setTimeout(() => {
    emits('answer', answer.value)
  }, 1_500)
  clearInterval(time)
}

onMounted(() => {
  time = setInterval(() => {
    if(t.value >= 0){
      t.value--
    }
  }, 1_000)

  timer = setTimeout(() => {
    answer.value = ''
    onAnswer()
  }, timeInResponse)
})

onUnmounted(() => {
  clearTimeout(timer)
  clearInterval(time)
})

</script>

<style>
.question{
  padding-top: 2rem;
}

.question li{
  list-style: none;
}
</style>