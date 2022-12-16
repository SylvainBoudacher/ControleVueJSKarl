<script setup>
import { defineProps } from "vue";
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="form__group">
    <label :for="name">{{ name }}</label>
    <component :is="as" :id="name" :name="name" />
  </div>
</template>
