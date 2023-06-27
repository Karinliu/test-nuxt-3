<template lang="pug">
section.videoplayer
  iframe.videoplayer__iframe(
    :src="`https://player.vimeo.com/video/${videoId}`"
    title="Video Player"
    frameborder="0"
    width="560"
    allowfullscreen
  )
</template>
  
<script setup>
const props = defineProps({
  videoId: {
    type: Number,
    required: true,
  },
});
</script>

<style lang="scss" scoped>
.videoplayer {
  &__iframe {
    width: 100%;
    height: 30rem;
  }
}
</style>
  