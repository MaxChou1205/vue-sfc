<template>
  <label class="relative cursor-pointer">
    <input
      type="checkbox"
      class="peer sr-only"
      :checked="modelValue"
      @change="emit('update:modelValue', $event.target.checked)"
    />

    <div
      class="relative w-full h-10 rounded-3xl bg-gray-400 peer-checked:bg-green-400 duration-200"
    ></div>
    <div
      class="absolute w-10 h-10 top-1/2 -translate-y-1/2 scale-75 bg-white rounded-full shadow-md duration-200 peer-checked:translate-x-full"
    ></div>
  </label>
</template>

<script setup>
const props = defineProps({
  modelValue: Boolean | String
});
const emit = defineEmits(["update:modelValue"]);
</script>

<style></style>
