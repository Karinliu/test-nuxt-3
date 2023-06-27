<template lang="pug">
label.lesson-complete-btn__label(
  :class="modelValue ? 'green' : 'gray' "
)
  input.hidden(
    type="checkbox"
    :value="modelValue"
    @input="() => $emit('update:modelValue', !modelValue)"
  ) 
  span.lesson-complete-btn__text {{ modelValue ? 'Completed!' : 'Mark as complete'}}
</template>

<script setup>
defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
});
defineEmits(['update:modelValue']);
</script>

<style lang="scss" scoped>
.lesson-complete-btn {
  &__label {
    display: inline-block;
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    cursor: pointer;
  }
}
.green {
  background-color: rgb(147, 231, 147);
}
.gray {
  background-color: rgb(164, 164, 164);
}
.hidden {
  display: none;
}
</style>
