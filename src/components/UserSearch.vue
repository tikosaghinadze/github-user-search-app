<script setup>
import { ref, defineEmits } from "vue";
import SearchIcon from "../assets/search-icon.svg";

const userName = ref("");
const userProfile = ref(null);
const error = ref(null);

const emit = defineEmits(["user-found"]);

const getUserProfile = async () => {
  try {
    const response = await fetch(
      `https://api.github.com/users/${userName.value}`
    );
    const data = await response.json();

    if (response.ok) {
      userProfile.value = data;
      error.value = null;
      emit("user-found", userProfile.value);
    } else {
      userProfile.value = null;
      error.value = "No Results";
    }
  } catch (err) {
    console.log(err);
    error.value = "An error occurred";
  }
};
</script>

<template>
  <div
    class="bg-white w-full flex items-center justify-between p-[9.5px] rounded-[15px] cursor-pointer dark:bg-[#1E2A47]"
  >
    <div class="w-[300px] flex items-center gap-[4px] md:gap-[23px]">
      <img class="w-5 h-5 md:w-5 md:h-6" :src="SearchIcon" alt="search icon" />
      <input
        v-model="userName"
        @keydown.enter="getUserProfile"
        class="outline-none placeholder:text-center w-full placeholder:text-[13px] md:placeholder:text-[18px] placeholder:text-[#4B6A9B] placeholder:font-[Space Mono] text-[13px] md:text-[18px] text-[#222731] font-[Space Mono] dark:bg-[#1E2A47] dark:text-white dark:placeholder:text-white"
        type="text"
        placeholder="Search GitHub username…"
      />
    </div>
    <div class="flex justify-center items-center gap-6">
      <h4 class="text-[15px] font-bold text-[#F74646]">{{ error }}</h4>
      <button
        class="bg-[#0079FF] text-[14px] text-bold text-white text-base rounded-[10px] font[Space Mono] px-[18px] py-3 md:px-6 md:py-3 hover:bg-[#60ABFF]"
        @click="getUserProfile"
      >
        Search
      </button>
    </div>
  </div>
</template>
