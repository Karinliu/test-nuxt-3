<template lang="pug">
div.login
  h1 Log in to {{ title }}
  button.login__btn Log in with Github
</template>

<script setup>
const { title } = useCourse();
</script>

<style lang="scss">
.login {
  &__btn {
    color: #5656e4;
    text-decoration: none;
    border: 0.1rem solid #5656e4;
    padding: 0.5rem;
    border-radius: 0.5rem;
    transition: 0.2s;
    margin-right: 1rem;
    cursor: pointer;
    &:hover,
    &:focus {
      background-color: #5656e4;
      color: white;
    }
  }
}
</style>
