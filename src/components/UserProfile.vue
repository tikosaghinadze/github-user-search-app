<script setup>
import { defineProps } from "vue";
defineProps(["userProfile"]);

const formatDate = (dateString) => {
  const options = { year: "numeric", month: "short", day: "numeric" };
  return new Date(dateString).toLocaleDateString("en-GB", options);
};
</script>

<template>
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
          <img src="../assets/office-building.svg" alt="office building icon" />
          <span class="text-[#4B6A9B] text-[13px] md:text-[15px]">{{
            userProfile.company || "Not available"
          }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>
