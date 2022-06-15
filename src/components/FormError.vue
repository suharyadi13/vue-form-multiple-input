<template>
  <p v-if="errors.length" class="help is-danger">
    <ul>
      <li v-for="error in errors" :key="error">{{error}}</li>
    </ul>
  </p> 
</template>

<script>
export default {
  name: "FormError",
  props: {
    errors: Array
  }
};
</script>
