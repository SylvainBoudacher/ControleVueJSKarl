<script setup>
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
</script>

<template></template>

<style></style>
