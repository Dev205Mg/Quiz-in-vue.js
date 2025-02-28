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
          v-model="answer"
          :correctaAnswer="question.correct_answer"
        />
      </li>
    </ul>
    <button 
      @click="emits('answer', answer)"
      :disabled="!hasAnswer"
      >
      Question suivante
    </button>
  </div>
</template>

<script setup>
import { shuffleArray } from '@/functions/array';
import { computed, ref } from 'vue';
import Answer from './Answer.vue';

const props = defineProps({
  question: Object
})
const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)
const randomChoice = computed(() => shuffleArray(props.question.choices))
</script>

<style>
.question{
  padding-top: 2rem;
}

.question button{
  margin-left: auto;
  display: block;
}
</style>