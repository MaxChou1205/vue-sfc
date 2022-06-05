<template>
  <div class="w-full p-4 bg-gray-200 rounded-lg">
    <slot
      :minVal="minVal"
      :maxVal="maxVal"
      :currentVal="currentVal"
      :percent="percent"
      class="mb-2"
    />
    <div class="w-full h-4 bg-gray-400 rounded-full">
      <div
        class="h-4 bg-green-400 rounded-full duration-500"
        :style="{ width: percent + '%' }"
      ></div>
    </div>
  </div>
</template>

<script setup>
import { computed, toRefs } from "vue";

const props = defineProps({
  minVal: Number | String,
  maxVal: Number | String,
  currentVal: Number | String
});

const { minVal, maxVal, currentVal } = toRefs(props);

const percent = computed(() => {
  return currentVal.value <= minVal.value
    ? 0
    : ((currentVal.value - minVal.value) * 100) / (maxVal.value - minVal.value);
});
</script>

<style></style>
