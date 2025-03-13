<script setup></script>

<template>
  <div class="max-w-[573px]">
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
            class="outline-none placeholder:text-[18px] placeholder:text-[#4B6A9B] placeholder:font-[Space Mono] text-[18px] text-[#222731] font-[Space Mono]"
            type="text"
            placeholder="Search GitHub username…"
          />
        </div>
        <div class="flex justify-center items-center gap-6">
          <h4 class="text-[15px] font-bold text-[#F74646]">No Results</h4>
          <button
            class="bg-[#0079FF] text-bold text-white text-base rounded-[10px] font[Space Mono] px-6 py-3 hover:bg-[#60ABFF]"
          >
            Search
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
