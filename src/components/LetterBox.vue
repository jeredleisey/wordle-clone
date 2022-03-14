<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps({
  letter: {
    type: String,
    default: '',
  },
  color: {
    type: String,
    default: '',
  },
});

const pulse = ref(false);
const selected = ref(props.letter);

watch(
  () => props.letter,
  (selected, prevSelected) => {
    if (selected && selected.length > 0) {
      pulse.value = true;
      setTimeout(() => {
        pulse.value = false;
      }, 100);
    }
  }
);
</script>

<template>
  <div
    class="col-span-1 flex items-center justify-center h-16 uppercase border-2 border-gray-200 transition-all duration-300 transform"
    :class="{
      'border-gray-400': color == '' && letter.length > 0,
      'border-gray-500 bg-gray-500 text-white': color == 'gray',
      'border-green-600 bg-green-600 text-white': color == 'green',
      'border-yellow-500 bg-yellow-500 text-white': color == 'yellow',
    }"
  >
    {{ letter }}
  </div>
</template>
