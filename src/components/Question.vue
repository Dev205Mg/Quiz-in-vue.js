<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li 
        v-for="(choice, index) in question.choices"
        :key="choice"
        >
        <label :for="`answer${index}`">
          <input 
            type="radio" 
            name="answer" 
            :id="`answer${index}`"
            v-model="answer"
            :value="choice"
          >
          {{ choice }}
        </label>
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
import { computed, ref } from 'vue';

const props = defineProps({
  question: Object
})
const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)
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