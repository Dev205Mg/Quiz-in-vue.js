<template>
  <label :for="id" :class="classes">
    <input 
      :disabled="disabled"
      type="radio" 
      name="answer" 
      :id="id"
      v-model="model"
      :value="value"
    >
    {{ value }}
  </label>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  id: String,
  disabled: Boolean,
  value: String,
  correctaAnswer: String
})

const model = defineModel()
const classes = computed(() => ({
  disabled: props.disabled,
  right: props.disabled && props.value === props.correctaAnswer,
  wrong: props.disabled && props.value !== props.correctaAnswer && model.value === props.value,
}))
</script>

<style>
.disabled{
  opacity: .5;
}

.right{
  opacity: 1;
  color: green;
}

.wrong{
  opacity: 1;
  color: red;
}
</style>