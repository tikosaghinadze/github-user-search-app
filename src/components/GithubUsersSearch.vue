<script setup>
import { ref } from "vue";
import darkIcon from "../assets/dark-icon.svg";
import lightIcon from "../assets/light-icon.svg";
const userName = ref("");
const userProfile = ref(null);
const error = ref(null);
const isDarkMode = ref(false);

const getUserProfile = async () => {
  try {
    const response = await fetch(
      `https://api.github.com/users/${userName.value}`
    );
    const data = await response.json();

    if (response.ok) {
      userProfile.value = data;
      error.value = null;
    } else {
      userProfile.value = null;
      error.value = "No Results";
    }
  } catch (err) {
    console.log(err);
    error.value = "An error occurred";
  }
};

const formatDate = (dateString) => {
  const options = { year: "numeric", month: "short", day: "numeric" };
  return new Date(dateString).toLocaleDateString("en-GB", options);
};

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
  <div class="w-[327px] md:w-[573px] lg:w-[730px]">
    <div class="mb-4 flex flex-col gap-9">
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
      <div
        class="flex justify-between items-center bg-white p-[9.5px] rounded-[15px] cursor-pointer dark:bg-[#1E2A47]"
      >
        <div class="flex justify-center items-center gap-6">
          <img src="../assets/search-icon.svg" alt="search icon" />
          <input
            v-model="userName"
            @keydown.enter="getUserProfile"
            class="outline-none placeholder:text-[13px] md:placeholder:text-[18px] placeholder:text-[#4B6A9B] placeholder:font-[Space Mono] text-[13px] md:text-[18px] text-[#222731] font-[Space Mono] dark:bg-[#1E2A47] dark:text-white placeholder:text-white"
            type="text"
            placeholder="Search GitHub username…"
          />
        </div>
        <div class="flex justify-center items-center gap-6">
          <h4 class="text-[15px] font-bold text-[#F74646]">{{ error }}</h4>
          <button
            class="bg-[#0079FF] text-[14px] text-bold text-white text-base rounded-[10px] font[Space Mono] px-[18px] py-3 lg:px-6 lg:py-3 hover:bg-[#60ABFF]"
            @click="getUserProfile"
          >
            Search
          </button>
        </div>
      </div>
    </div>
    <div v-if="userProfile" class="bg-white rounded-[15px] p-6 md:p-12">
      <div class="flex gap-[37px]">
        <img
          class="rounded-full lg:w-[117px] lg:h-[117px] w-[70px] h-[70px]"
          :src="userProfile.avatar_url"
          alt="user profile pic"
        />
        <div class="flex md:justify-between md:flex-row flex-col w-full">
          <div>
            <h1 class="font-bold lg:text-[26px] text-4 text-[#2B3442]">
              {{ userProfile.name }}
            </h1>
            <h2 class="text-base text-[#0079FF]">{{ userProfile.login }}</h2>
          </div>
          <p class="text-[#697C9A] lg:text-[15px] text-[13px]">
            Joined {{ formatDate(userProfile.created_at) }}
          </p>
        </div>
      </div>
      <div class="lg:pl-[148px] mt-8 flex flex-col gap-8 md:pl-0 md:mt-6">
        <p class="lg:text-[15px] text-[13px] leading-[25px] text-[#4B6A9B]">
          {{ userProfile.bio || "This profile has no Bio" }}
        </p>

        <ul
          class="bg-[#F6F8FF] w-full flex gap-8 md:gap-[99px] py-[15px] px-8 rounded-[10px]"
        >
          <li class="text-[11px] md:text-[13px] text-[#4B6A9B]">
            Repos <br />
            <span class="text-[16px] md:text-[22px] font-bold text-[#2B3442]">{{
              userProfile.public_repos
            }}</span>
          </li>
          <li class="text-[11px] md:text-[13px] text-[#4B6A9B]">
            Followers <br /><span
              class="text-[16px] md:text-[22px] font-bold text-[#2B3442]"
              >{{ userProfile.followers }}</span
            >
          </li>
          <li class="text-[11px] md:text-[13px] text-[#4B6A9B]">
            Following <br />
            <span class="text-[16px] md:text-[22px] font-bold text-[#2B3442]">{{
              userProfile.following
            }}</span>
          </li>
        </ul>

        <ul class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-y-[21px]">
          <li class="flex items-center gap-[19.2px]">
            <img src="../assets/location-icon.svg" alt="location icon" />
            <span class="text-[#4B6A9B] text-[13px] md:text-[15px]">{{
              userProfile.location || "Not available"
            }}</span>
          </li>
          <li class="flex items-center gap-[19.2px] cursor-pointer">
            <img src="../assets/twitter.svg" alt="twitter icon" />
            <span class="text-[#4B6A9B] text-[13px] md:text-[15px]">{{
              userProfile.twitter_username || "Not available"
            }}</span>
          </li>
          <li class="flex items-center gap-[19.2px] cursor-pointer">
            <img src="../assets/link-icon.svg" alt="url icon" />
            <a
              :href="userProfile.blog"
              class="text-[#4B6A9B] text-[13px] md:text-[15px]"
            >
              {{ userProfile.blog || "Not available" }}
            </a>
          </li>
          <li class="flex items-center gap-[19.2px]">
            <img
              src="../assets/office-building.svg"
              alt="office building icon"
            />
            <span class="text-[#4B6A9B] text-[13px] md:text-[15px]">{{
              userProfile.company || "Not available"
            }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style>
.dark {
  background-color: #141d2f;
  /* color: white; */
}
</style>
