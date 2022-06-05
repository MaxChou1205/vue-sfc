<template>
  <div class="max-w-[1208px] p-8 mx-auto">
    <div class="w-200 mt-10">
      <input type="range" v-model="val" :min="min" :max="max" />
      <ProgressBar
        :minVal="min"
        :maxVal="max"
        :currentVal="val"
        v-slot="{ percent }"
      >
        <div class="text-center mb-4">已下載 {{ percent }}</div>
        <div class="text-center mb-4">正在準備資源 ({{ val }} / {{ max }})</div>
      </ProgressBar>
    </div>

    <div class="w-40 mt-10">
      <BaseButton text="我是按鈕">
        <template v-slot:left>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M10 19l-7-7m0 0l7-7m-7 7h18"
            />
          </svg>
        </template>
        <template v-slot:right>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M17 8l4 4m0 0l-4 4m4-4H3"
            />
          </svg>
        </template>
      </BaseButton>
    </div>

    <div class="w-200 mt-10">
      <AccordionMenuItem
        v-for="item in list.items"
        :key="list.groupName.concat('-', item.name)"
        :itemName="item.name"
      >
        <template v-slot:itemText>{{ item.content }}</template>
      </AccordionMenuItem>
    </div>

    <div class="w-200 mt-10">
      <AccordionMenuItem
        v-for="item in faq.links"
        :key="list.groupName.concat('-', item.name)"
        :itemName="item.name"
      >
        <template v-slot:itemContent>
          <div
            v-for="text in item.contents"
            :key="text"
            class="p-3 hover:bg-gray-100 border-t first:border-0"
          >
            {{ text }}
          </div>
        </template>
      </AccordionMenuItem>
    </div>

    <div class="w-80 mt-10 mx-auto">
      <SimpleCalendar />
    </div>

    <div class="w-80 mt-10 mx-auto">
      <BaseButton text="開啟modal" color="blue" @click="showModal = true" />
    </div>
    <Modal :show="showModal" title="注意" @close="showModal = false"
      ><template v-slot:itemContent>
        <div class="text-xl text-red-900">第一段文字</div>
        <p class="text-sm text-gray-500">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Soluta, at.
          Repellendus sint perspiciatis voluptatem vero sit ratione aperiam aut
          rerum, neque asperiores porro quis repudiandae ipsum quam, vel
          necessitatibus deserunt temporibus eaque consectetur explicabo est
          dolore ad. Qui nihil iste sed, facere, doloremque cumque sunt illum
          iure, harum omnis voluptate!
        </p>
      </template>
    </Modal>

    <div class="w-80 mt-10 mx-auto">
      <BaseButton text="開啟modal2" color="blue" @click="showModal2 = true" />
    </div>
    <Modal :show="showModal2" title="這是標題" @close="showModal2 = false">
      這是內容
    </Modal>

    <div class="w-20 mt-10 mx-auto">
      <div>{{ switcherChecked }}</div>
      <Switcher v-model="switcherChecked" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
// import HelloWorld from './components/HelloWorld.vue'
import ProgressBar from "@/components/ProgressBar.vue";
import BaseButton from "./components/BaseButton.vue";
import AccordionMenuItem from "./components/AccordionMenuItem.vue";
import SimpleCalendar from "./components/SimpleCalendar.vue";
import Modal from "./components/Modal.vue";
import Switcher from "./components/Switcher.vue";

// ProgressBar
const min = ref(0);
const max = ref(100);
const val = ref(0);

// AccordionMenuItem
const list = ref({
  groupName: "Abouts",
  items: [
    {
      name: "關於兔兔教",
      content:
        "不是邪教，但不太正常 (？)。 不過可以為你在此獻上教義 ... (住嘴！)"
    },
    { name: "關於 Tailwind CSS", content: "超讚了啦，不用真是太可惜了！" },
    { name: "關於手風琴", content: "流浪到淡水時有機會可以看到。" },
    { name: "關於兔兔", content: "你想知道的太多了，去擲筊問神吧！！！" }
  ]
});
const faq = ref({
  groupName: "FAQ",
  links: [
    { name: "四大超商", contents: ["7-11", "全家", "萊爾富", "OK"] },
    {
      name: "付款方式",
      contents: ["現金", "ATM", "信用卡", "LINE PAY", "五倍券"]
    },
    { name: "取貨方式", contents: ["宅配", "超商取貨"] }
  ]
});

// Modal
const showModal = ref(false);
const showModal2 = ref(false);

// Switcher
const switcherChecked = ref(false);
</script>

<style></style>
