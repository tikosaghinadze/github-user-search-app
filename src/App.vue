<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import UserSearch from "./components/UserSearch.vue";
import UserProfile from "./components/UserProfile.vue";

const userProfile = ref(null);
</script>

<template>
  <div
    class="w-full min-h-screen flex justify-center items-center bg-[#F6F8FF] dark:bg-[#141D2F]"
  >
    <div class="w-[327px] md:w-[573px] lg:w-[730px]">
      <div class="mb-4 flex flex-col gap-9">
        <Header />
        <UserSearch @user-found="userProfile = $event" />
      </div>
      <UserProfile :userProfile="userProfile" />
    </div>
  </div>
</template>

<style>
.dark {
  background-color: #141d2f;
  /* color: white; */
}
</style>
