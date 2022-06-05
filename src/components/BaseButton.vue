<template>
  <div
    :class="[
      'flex justify-around items-center',
      'rounded-xl',
      'px-4 py-2',
      'cursor-pointer',
      'duration-300',
      'hover:scale-105 active:scale-95',
      'text-white',
      colorSelector
    ]"
  >
    <slot name="left" />
    {{ text }}
    <slot name="right" />
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  text: String,
  color: {
    type: String,
    default: "gray"
  }
});

const colorSelector = computed(() => {
  return {
    gray: "bg-gray-400 hover:bg-gray-300 active:bg-gray-500",
    green: "bg-green-400 hover:bg-green-300 active:bg-green-500",
    blue: "bg-blue-400 hover:bg-blue-300 active:bg-blue-500",
    red: "bg-red-400 hover:bg-red-300 active:bg-red-500",
    yellow: "bg-yellow-400 hover:bg-yellow-300 active:bg-yellow-500"
  }[props.color];
});
</script>

<style></style>
