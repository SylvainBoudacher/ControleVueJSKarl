<script setup>
import { defineProps, reactive, ref } from "vue";

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

// Methods
const toggleSubmit = (value) => (isSubmitting.value = value);

const handleSubmit = async (e) => {
  e.preventDefault();
  isSubmitting.value = true;
  const potentialErrors = props.validate(values);

  if (Object.keys(potentialErrors).length > 0) {
    isSubmitting.value = false;
    for (const [key, value] of Object.entries(potentialErrors)) {
      errors[key] = value;
    }
    return;
  }

  await props.onSubmit(values, toggleSubmit);

  isSubmitting.value = false;
};
</script>

<template>
  <form @submit="handleSubmit">
    <slot :values="values" :errors="errors" :isSubmitting="isSubmitting" />
  </form>
</template>

<style></style>
