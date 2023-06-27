<template lang="pug">
NuxtLayout
  .error
    .error__container(v-if="error.statusCode === '404'")
      h1.error__title 404
      p.error__text That page doesn't exist.
    .error__container(v-else)
      h1.error__title Oops 
      p.error__text It looks like something broke 
      p.error__text Sorry about that.
    .error__container
      p.error__message 
        span.error__message-span {{ error.message }}
      nuxt-link.error__btn(@click="handleError") Return to the first lesson
</template>

<script setup>
const error = useError();

const handleError = () => {
  clearError({
    redirect:
      "/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3",
  });
};
</script>

<style lang="scss" scoped>
.error {
  width: 50rem;
  margin: auto;
  &__message {
    margin-bottom: 1rem;
    &-span {
      font-weight: bold;
    }
  }
  &__btn {
    display: inline-block;
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
