<template>
  <LikertScale
    field-id="test-scale"
    :options="options"
    :questions="questions"
    is-required
    unique-two-d
    :values="values"
    v-on:blur="handleBlur($event)"
    v-on:change="handleChange($event)"
    v-on:invalid="handleInvalid($event)" />
</template>

<script setup>
import { ref } from 'vue';
import LikertScale from './components/LikertScale.vue'

const options = ref([
  { value: '0', label: 'Very bad' },
  { value: '1', label: 'Bad' },
  { value: '2', label: 'OK' },
  { value: '3', label: 'Good' },
  { value: '4', label: 'Very good' },
  { value: '-1', label: 'Prefer not to say' },
]);

const questions = ref([
  { id: 'good-xmas', label: 'How good is Christmas' },
  { id: 'food', label: 'What is the quality of food at your Christmas lunch' },
  { id: 'company', label: 'How well do your family get on at Christmas' },
]);

const values = ref({
  'good-xmas': 2,
  food: 4,
  company: -1,
});

const localValues = ref({});
const invalid = ref(false);

const handleChange = (event) => {
  console.group('App.handleChange()');
  console.log('invalid.value (before):', invalid.value);
  console.log('localValues.value (before):', localValues.value);
  console.log('event:', event);
  localValues.value = event;
  console.log('localValues.value (after):', localValues.value);
  console.log('invalid.value (after):', invalid.value);
  console.groupEnd();
}

const handleBlur = (event) => {
  console.group('App.handleBlur()');
  console.log('event:', event);
  console.groupEnd();
}

const handleInvalid = (event) => {
  console.group('App.handleInvalid()');
  console.log('invalid.value (before):', invalid.value);
  invalid.value = event;
  console.log('invalid.value (after):', invalid.value);
  console.groupEnd();
}
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
