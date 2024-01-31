<template>
  <tr>
    <th :id="rowId">
      {{ question.label }}
    </th>
    <td
      v-for="option in options"
      :key="option.value">
      <input
        :aria-labelledby="`${labeledBy} ${rowId} ${fieldId}--${option.value}`"
        :checked="option.value === value"
        :data-quid="question.id"
        :disabled="disabled"
        :id="getInputID(option.value)"
        :name="radioName"
        :required="isRequired"
        type="radio"
        :value="option.value"
        v-on:change="handleChange($event)"
        class="visually-hidden" />
      <label class="radio-icon" :for="getInputID(option.value)">{{ option.label }}</label>
    </td>
  </tr>
</template>

<script setup>
import { computed } from 'vue';

const emit = defineEmits(['change']);

const props = defineProps({
  disabled: { type: Boolean, required: false, default: false },
  fieldId: { type: String, required: true },
  labeledBy: { type: String, required: false, default: '' },
  options: { type: Array, required: true },
  question: { type: Object, required: true },
  isRequired: { type: Boolean, required: false, default: false },
  value: { type: String, required: false, default: '' },
});

const rowId = computed(() => `${props.fieldId}--${props.question.id}`);
const radioName = computed(() => `radio-${rowId.value}`);

const getInputID = (value) => `${props.fieldId}-${props.question.id}--${value}`;

const handleChange = (event) => {
  emit('change', { id: props.question.id, value: event.target.value });
};
</script>
