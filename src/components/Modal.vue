<template>
  <Teleport to="body">
    <div
      class="fixed top-0 left-0 w-screen h-screen overflow-hidden flex justify-center items-center duration-200"
      :class="show ? 'opacity-100 scale-100' : 'opacity-0 scale-0'"
    >
      <div class="absolute top-0 left-0 w-full h-full bg-black/50"></div>
      <div class="w-full max-w-md bg-white rounded-lg overflow-hidden z-10">
        <div class="p-3 flex justify-between items-center border-b">
          <div>{{ title }}</div>
          <div class="cursor-pointer" @click="close">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </div>
        </div>
        <div>
          <div class="p-3">
            <slot name="itemContent">
              <slot name="itemText">內容</slot>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
import { ref, watch, onMounted, onUnmounted } from "vue";

const props = defineProps({
  show: {
    type: Boolean,
    default: false
  },
  title: {
    type: String,
    required: true
  }
});

const emit = defineEmits(["close"]);

const close = () => {
  emit("close");
};

const pressEsc = e => {
  if (e.key === "Escape") close();
};

onMounted(() => {
  document.body.addEventListener("keyup", pressEsc);
});

onUnmounted(() => {
  document.body.removeEventListener("keyup", pressEsc);
});

watch(
  () => props.show,
  newVal => {
    if (newVal) document.body.style.overflow = "hidden";
    else document.body.style.overflow = "auto";
  }
);
</script>

<style></style>
