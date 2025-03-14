<script setup>
import { ref } from "vue";

const userName = ref("");
const userProfile = ref(null);
const error = ref(null);

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
</script>

<template>
  <div class="w-[730px] max-w-[730px]">
    <div class="mb-4 flex flex-col gap-9">
      <div class="flex justify-between items-center">
        <h2 class="text-[26px] text-[#222731] font-[Space Mono] font-bold">
          devfinder
        </h2>
        <div class="flex items-center justify-center gap-4 cursor-pointer">
          <h3
            class="tracking-[2.5px] font-[Space Mono] font-bold text-[#697C9A] text-[13px]"
          >
            DARK
          </h3>
          <img src="../assets/dark-icon.svg" alt="moon icon" />
        </div>
      </div>
      <div
        class="flex justify-between items-center bg-white p-[9.5px] rounded-[15px] cursor-pointer"
      >
        <div class="flex justify-center items-center gap-6">
          <img src="../assets/search-icon.svg" alt="search icon" />
          <input
            v-model="userName"
            @keydown.enter="getUserProfile"
            class="outline-none placeholder:text-[18px] placeholder:text-[#4B6A9B] placeholder:font-[Space Mono] text-[18px] text-[#222731] font-[Space Mono]"
            type="text"
            placeholder="Search GitHub username…"
          />
        </div>
        <div class="flex justify-center items-center gap-6">
          <h4 class="text-[15px] font-bold text-[#F74646]">{{ error }}</h4>
          <button
            class="bg-[#0079FF] text-bold text-white text-base rounded-[10px] font[Space Mono] px-6 py-3 hover:bg-[#60ABFF]"
            @click="getUserProfile"
          >
            Search
          </button>
        </div>
      </div>
    </div>
    <div v-if="userProfile" class="bg-white rounded-[15px] p-12">
      <div class="flex gap-[37px]">
        <img
          class="rounded-full w-[117px] h-[117px]"
          :src="userProfile.avatar_url"
          alt="user profile pic"
        />
        <div class="flex justify-between w-full">
          <div>
            <h1 class="font-bold text-[26px] text-[#2B3442]">
              {{ userProfile.name }}
            </h1>
            <h2 class="text-base text-[#0079FF]">{{ userProfile.login }}</h2>
          </div>
          <p class="text-[#697C9A] text-[15px]">
            Joined {{ formatDate(userProfile.created_at) }}
          </p>
        </div>
      </div>
      <div class="pl-[148px] flex flex-col gap-8">
        <p class="text-[15px] leading-[25px] text-[#4B6A9B]">
          {{ userProfile.bio || "This profile has no" }}
        </p>

        <ul class="bg-[#F6F8FF] flex gap-[99px] py-[15px] px-8 rounded-[10px]">
          <li class="text-[13px] text-[#4B6A9B]">
            Repos <br />
            <span class="text-[22px] font-bold text-[#2B3442]">{{
              userProfile.public_repos
            }}</span>
          </li>
          <li class="text-[13px] text-[#4B6A9B]">
            Followers <br /><span
              class="text-[22px] font-bold text-[#2B3442]"
              >{{ userProfile.followers }}</span
            >
          </li>
          <li class="text-[13px] text-[#4B6A9B]">
            Following <br />
            <span class="text-[22px] font-bold text-[#2B3442]">{{
              userProfile.following
            }}</span>
          </li>
        </ul>

        <ul class="flex flex-wrap justify-between gap-y-[21px]">
          <li class="flex w-1/2 items-center gap-[19.2px]">
            <img src="../assets/location-icon.svg" alt="location icon" />
            <span class="text-[#4B6A9B] text-[15px]">{{
              userProfile.location || "Not available"
            }}</span>
          </li>
          <li class="flex w-1/2 items-center gap-[19.2px] cursor-pointer">
            <img src="../assets/twitter.svg" alt="twitter icon" />
            <span class="text-[#4B6A9B] text-[15px]">{{
              userProfile.twitter_username || "Not available"
            }}</span>
          </li>
          <li class="flex w-1/2 items-center gap-[19.2px] cursor-pointer">
            <img src="../assets/link-icon.svg" alt="url icon" />
            <a :href="userProfile.blog" class="text-[#4B6A9B] text-[15px]">
              {{ userProfile.blog || "Not available" }}
            </a>
          </li>
          <li class="flex w-1/2 items-center gap-[19.2px]">
            <img
              src="../assets/office-building.svg"
              alt="office building icon"
            />
            <span class="text-[#4B6A9B] text-[15px]">{{
              userProfile.company || "Not available"
            }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
