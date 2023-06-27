<template lang="pug">
section
  nuxt-link.app-link(
    :to="firstLesson.path"
  ) Go to first lesson
</template>

<script setup>
const firstLesson = useFirstLesson();
</script>

<style lang="scss">
.app-link{
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
</style>
