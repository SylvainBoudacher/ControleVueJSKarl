<script setup>
import Formik from "./Formik.vue";
import Field from "./Field.vue";

const initialValues = {
  name: "",
  email: "",
  password: "",
};

const onSubmit = (values) => {
  alert(JSON.stringify(values, null, 2));
};

const validateValues = (values) => {
  const errors = {};
  name: if (!values.name) {
    errors.name = "Name is required";
    break name;
  }
  email: if (!values.email) {
    errors.email = "Email is required";
    break email;
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.email = "Email is invalid";
    break email;
  }
  password: if (!values.password) {
    errors.password = "Password is required";
    break password;
  } else if (values.password.length < 6) {
    errors.password = "Password must be at least 6 characters";
    break password;
  }
  return errors;
};
</script>

<template v-slot="default">
  <Formik
    :initialValues="initialValues"
    :validate="validateValues"
    :onSubmit="onSubmit"
  >
    <div class="main">
      <Field name="name" as="input" label="name" placeholder="name" />
      <Field name="email" as="input" label="email" placeholder="email" />
      <Field
        name="password"
        as="input"
        label="password"
        placeholder="password"
      />
      <button type="submit">Submit</button>
    </div>
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

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding-top: 1rem;
}
</style>
