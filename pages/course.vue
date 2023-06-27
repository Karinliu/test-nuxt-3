<template lang="pug">
section.course
  .course__title {{ title }}
  .course__block
    .course__block-section
      h2.course__secondary-title Chapters
      .course__chapters(
        v-for="chapter in chapters"
        :key="chapter.slug"
      )
        .course__chapters-title {{ chapter.title }}
        nuxt-link.course__chapters-url(
          v-for="(lesson, index) in chapter.lessons"
          :key="lesson.slug"
          :to="lesson.path"
        )
          span {{ index + 1 }}. 
          span {{ lesson.title }}
    .course__block-section
      NuxtErrorBoundary
        NuxtPage
        template(#error="{ error }")
          p Oh no, something went wrong with the lesson 
            code {{ error }}
          button(@click="resetError(error)") Reset
</template>

<script setup>
const { chapters, title } = useCourse();

const resetError = async (error) => {
  await navigateTo(
    "/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3"
  );
};
</script>

<style lang="scss" scoped>
.course {
  &__title {
    font-size: 1.5rem;
    line-height: 1.8rem;
    margin-bottom: 1rem;
    text-align: center;
  }
  &__secondary-title {
    font-size: 1.2rem;
    line-height: 1.5rem;
  }
  &__block {
    display: grid;
    grid-template-columns: 13rem 40rem;
    grid-gap: 1rem;
    justify-content: center;
    &-section {
      background-color: rgb(255, 255, 255);
      padding: 0.5rem;
    }
  }
  &__chapters {
    display: flex;
    flex-direction: column;
    margin-bottom: 1.5rem;
    &-title {
      font-weight: 800;
      font-style: italic;
      margin-bottom: 0.5rem;
    }
    &-url {
      margin-bottom: 0.5rem;
      color: #5656e4;
      text-decoration: none;
      &:hover,
      &:focus {
        color: #00009b;
      }
    }
  }
}
</style>
