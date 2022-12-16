<script setup>
import Formik from "./Formik.vue";
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <Formik
    :initialValues="{ name: '', email: '', password: '' }"
    :validate="validate"
    :onSubmit="onSubmit"
  />
</template>

<style>
@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
