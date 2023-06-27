<template lang="pug">
div.lesson
  .lesson__subtitle Lesson {{ chapter.number }} - {{ lesson.number }}
  h2 {{ lesson.title }}
  .lesson__container
    nuxt-link.lesson__download(v-if="lesson.sourceUrl" :to="lesson.sourceUrl") Download Source Code
    nuxt-link.lesson__download(v-if="lesson.downloadUrl" :to="lesson.downloadUrl") Download Video
    VideoPlayer(v-if="lesson.videoId" :videoId="lesson.videoId")
    .lesson__container-text {{ lesson.text }}
    LessonCompleteBtn(
      :model-value="isLessonComplete"
      @update:model-value="throw createError('Could not update');"
    )
</template>

<script setup>
import { useLocalStorage } from "@vueuse/core";

const course = useCourse();
const route = useRoute();

definePageMeta({
  middleware: [
    function ({ params }, from) {
      const course = useCourse();

      const chapter = course.chapters.find(
        (chapter) => chapter.slug === params.chapterSlug
      );

      if (!chapter) {
        return abortNavigation(
          createError({
            statusCode: 404,
            message: "Chapter not found",
          })
        );
      }

      const lesson = chapter.lessons.find(
        (lesson) => lesson.slug === params.lessonSlug
      );

      if (!lesson) {
        return abortNavigation(
          createError({
            statusCode: 404,
            message: "Lesson not found",
          })
        );
      }
    },
    "auth",
  ],
});

const title = computed(() => {
  return `${lesson.value.title}`;
});

const chapter = computed(() => {
  return course.chapters.find(
    (chapter) => chapter.slug === route.params.chapterSlug
  );
});

const lesson = computed(() => {
  return chapter.value.lessons.find(
    (lesson) => lesson.slug === route.params.lessonSlug
  );
});

const progress = useLocalStorage("progress", []);

const isLessonComplete = computed(() => {
  if (!progress.value[chapter.value.number - 1]) {
    return false;
  }
  if (!progress.value[chapter.value.number - 1][lesson.value.number - 1]) {
    return false;
  }
  return progress.value[chapter.value.number - 1][lesson.value.number - 1];
});
const toggleComplete = () => {
  if (!progress.value[chapter.value.number - 1]) {
    progress.value[chapter.value.number - 1] = [];
  }
  progress.value[chapter.value.number - 1][lesson.value.number - 1] =
    !isLessonComplete.value;
};

useHead({
  title,
});
</script>

<style lang="scss" scoped>
.lesson {
  &__secondary-title {
    font-size: 1.2rem;
    line-height: 1.5rem;
  }
  &__subtitle {
    text-transform: uppercase;
  }
  &__download {
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
