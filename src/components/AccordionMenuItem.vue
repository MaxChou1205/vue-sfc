<template>
  <label
    class="px-4 py-2 border border-gray-300 hover:bg-gray-100 flex justify-between items-center cursor-pointer"
  >
    <input type="checkbox" class="sr-only" v-model="checked" />
    <div :class="['transition-all', checked && 'text-green-500']">
      {{ itemName }}
    </div>
    <div
      class="w-9 h-9 hover:bg-gray-200 rounded-full flex justify-center items-center"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        :class="['h-6 w-6 transition-all', checked && '-rotate-180']"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M19 9l-7 7-7-7"
        />
      </svg>
    </div>
  </label>
  <div
    :class="[
      'border border-t-0 border-gray-300 overflow-hidden transition-all',
      checked ? 'max-h-[300px]' : 'max-h-0 border-0'
    ]"
  >
    <slot name="itemContent">
      <div class="p-4 text-gray-600">
        <slot name="itemText">內容</slot>
      </div>
    </slot>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  itemName: String
});

const checked = ref(false);
</script>

<style></style>
