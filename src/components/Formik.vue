<script setup>
import { defineProps, provide, reactive, ref } from "vue";

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function,
    required: true,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
});

// States
const values = reactive(props.initialValues);
const errors = reactive({});
const isSubmitting = ref(false);

// Injectables
const inputUpdated = (id, value) => {
  values[id] = value;
};

provide("values", { values, inputUpdated });

// Methods
const toggleSubmit = (value) => (isSubmitting.value = value);

const handleSubmit = (e) => {
  e.preventDefault();
  isSubmitting.value = true;
  const potentialErrors = props.validate(values);

  for (const key in errors) {
    delete errors[key];
  }

  if (Object.keys(potentialErrors).length > 0) {
    for (const [key, value] of Object.entries(potentialErrors)) {
      errors[key] = value;
    }
    return;
  }

  props.onSubmit(values, toggleSubmit);

  isSubmitting.value = false;
};
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <div>
      <p>Values :</p>
      <pre>
      {{ values }}
    </pre
      >
      <hr />
      <p>Errors :</p>
      <ul>
        <li v-for="(error, field) in errors" :key="field">{{ error }}</li>
      </ul>
      <hr />
    </div>
    <slot :values="values" :errors="errors" :isSubmitting="isSubmitting" />
  </form>
</template>

<style></style>
