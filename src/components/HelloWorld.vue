<script setup>
import Formik from "./Formik.vue";
import Field from "./Field.vue";

const initialValues = {
  name: "",
  email: "",
  password: "",
  textarea: "",
  select: "",
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
  textarea: if (!values.textarea) {
    errors.textarea = "Textarea is required";
    break textarea;
  }
  select: if (!values.select) {
    errors.select = "Select is required";
    break select;
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
      <Field name="textarea" as="textarea" label="textarea" />
      <Field name="select" as="select" label="select">
        <option value="">Select</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
      </Field>
      <button type="submit">Submit</button>
    </div>
  </Formik>
</template>

<style>
.main {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 1rem;
  padding-top: 1rem;
  width: 100%;
}
</style>
