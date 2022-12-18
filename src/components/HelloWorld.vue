<script setup>
import Formik from "./Formik.vue";
import Field from "./Field.vue";
defineProps({
  msg: {
    type: String,
    required: true,
  },
});

const onSubmit = (values) => {
  alert(JSON.stringify(values, null, 2));
};
</script>

<template>
  <Formik
    :initialValues="{ name: '', email: '', password: '' }"
    :validate="
      (values) => {
        const errors = {};
        if (!values.name) {
          errors.name = 'Name is required';
        }
        if (!values.email) {
          errors.email = 'Email is required';
        }
        if (!values.password) {
          errors.password = 'Password is required';
        }
        return errors;
      }
    "
    :onSubmit="onSubmit"
  >
    <template #default="{ values, errors, isSubmitting }">
      <div class="form">
        <div class="form__group">
          <label for="name">Name</label>
          <input
            type="text"
            id="name"
            v-model="values.name"
            :class="{ error: errors.name }"
          />
          <p class="error" v-if="errors.name">{{ errors.name }}</p>
        </div>
        <div class="form__group">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            v-model="values.email"
            :class="{ error: errors.email }"
          />
          <p class="error" v-if="errors.email">{{ errors.email }}</p>
        </div>
        <div class="form__group">
          <label for="password">Password</label>
          <input
            type="password"
            id="password"
            v-model="values.password"
            :class="{ error: errors.password }"
          />
          <p class="error" v-if="errors.password">{{ errors.password }}</p>
        </div>
        <div class="form__group">
          <button type="submit" :disabled="isSubmitting">
            {{ isSubmitting ? "Submitting..." : "Submit" }}
          </button>
        </div>
      </div>
    </template>
  </Formik>
</template>

<style>
@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}

.greetings {
  text-align: center;
  margin-bottom: 2rem;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form__group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 1rem;
}
</style>
