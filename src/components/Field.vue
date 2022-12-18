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
  background: 0;
  outline: none;
  width: 60vw;
  max-width: 200px;
  font-size: 1.5em;
}

textarea {
  border: 1px solid red;
  width: 60vw;
  max-width: 200px;
}

select {
  width: 60vw;
  max-width: 200px;
  border: 1px solid blue;
}
</style>
