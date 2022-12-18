<script setup>
import { inject } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: [Object, String],
    required: true,
  },
});

const formik = inject("formik");
</script>

<template>
  <component :name="name" :is="props.as" v-model="formik.values[props.name]">
    <slot />
  </component>
</template>

<style scoped>
input {
  border: 1px solid red;
}

textarea {
  border: 1px solid red;
}

select {
  border: 1px solid red;
}

label {
  color: red;
}
</style>
