<template>
  <div class="flex flex-col rounded-xl border border-gray-200 overflow-hidden">
    <div
      class="p-3 flex items-center justify-around bg-blue-600 text-white font-bold border-b"
    >
      <div class="text-xl">{{ year }} {{ month }}月</div>
      <div class="flex gap-2 ml-auto">
        <svg
          @click="changeMonth(-1)"
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 cursor-pointer"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M9.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L7.414 9H15a1 1 0 110 2H7.414l2.293 2.293a1 1 0 010 1.414z"
            clip-rule="evenodd"
          />
        </svg>
        <svg
          @click="changeMonth(1)"
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 cursor-pointer"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z"
            clip-rule="evenodd"
          />
        </svg>
      </div>
    </div>

    <div class="p-2 mt-2 grid grid-cols-7 p gap-2 place-items-center">
      <div v-for="day in weekDays" :key="day">{{ day }}</div>
    </div>

    <div
      class="p-2 grid grid-cols-7 gap-2 gap-y-4 place-items-center cursor-default"
    >
      <!-- last month -->
      <div v-for="d in lastMonth" :key="d" class="text-gray-400">
        {{ d }}
      </div>

      <!-- this month -->
      <div
        v-for="d in thisMonth"
        :key="d"
        class="w-10 h-10 flex justify-center items-center rounded-full"
        :class="
          year === today.getFullYear() &&
          month - 1 === today.getMonth() &&
          d === today.getDate()
            ? 'bg-blue-600 text-white font-bold'
            : 'hover:bg-gray-200'
        "
      >
        {{ d }}
      </div>

      <!-- next month -->
      <div v-for="d in nextMonth" :key="d" class="text-gray-500">
        {{ d }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const weekDays = ref(["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa"]);
const today = ref(new Date());
const currentDate = ref(new Date());

const year = computed(() => {
  return currentDate.value.getFullYear();
});

const month = computed(() => {
  return currentDate.value.getMonth() + 1;
});

const lastMonth = computed(() => {
  const days = [];

  const current = new Date(year.value, month.value - 1, 1);
  const wd = current.getDay();

  for (let i = wd; i > 0; i--) {
    const temp = new Date(current);
    temp.setDate(current.getDate() - i);
    days.push(temp.getDate());
  }

  return days;
});

const thisMonth = computed(() => {
  const days = [];

  const totalDays = new Date(year.value, month.value, 0).getDate();

  for (let i = 1; i <= totalDays; i++) {
    days.push(i);
  }

  return days;
});

const nextMonth = computed(() => {
  const count = 42 - lastMonth.value.length - thisMonth.value.length;

  const days = [];

  for (let i = 1; i <= count; i++) {
    days.push(i);
  }

  return days;
});

const changeMonth = val => {
  let result = new Date();
  result.setFullYear(
    currentDate.value.getFullYear(),
    currentDate.value.getMonth() + val,
    currentDate.value.getDate()
  );
  currentDate.value = result;
};
</script>

<style></style>
