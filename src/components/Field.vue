<script setup>
//create a Field component that will be used in the Formik component with Dynamic Components and only name and as props
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
