<script setup>
import { ref } from "vue";
import darkIcon from "../assets/dark-icon.svg";
import lightIcon from "../assets/light-icon.svg";

const isDarkMode = ref(false);

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.documentElement.classList.add("dark");
  } else {
    document.documentElement.classList.remove("dark");
  }
};
</script>

<template>
  <header class="flex justify-between items-center">
    <h2
      class="text-[26px] text-[#222731] dark:text-white font-[Space Mono] font-bold"
    >
      devfinder
    </h2>
    <div
      @click="toggleDarkMode"
      class="flex items-center justify-center gap-4 cursor-pointer"
    >
      <h3
        class="tracking-[2.5px] font-[Space Mono] font-bold text-[#697C9A] text-[13px] dark:text-white dark:hover:text-[#90A4D4]"
      >
        {{ isDarkMode ? "LIGHT" : "  DARK" }}
      </h3>
      <img
        class="text-red-500 fill-red-500 stroke-red-500"
        :src="isDarkMode ? lightIcon : darkIcon"
        alt="dark-light themes"
      />
    </div>
  </header>
</template>
