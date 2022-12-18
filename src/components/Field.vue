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

const { values, inputUpdated } = inject("values");
</script>

<template>
  <component
    :name="name"
    :is="props.as"
    :value="values[name]"
    @input="inputUpdated(name, $event.target.value)"
  >
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
</style>
