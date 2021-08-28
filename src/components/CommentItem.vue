<template>
  <div class="flex">
    <img
      :src="avatar"
      alt=""
      class="w-12 h-12 mr-4 rounded-full"
    >
    <div>
      <p>{{ user }}</p>
      <p class="text-gray-600 text-sm">{{ time }}</p>
    </div>

    <span class="ml-auto">
      <svg
        t="1627738605987"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="2010"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="30"
        height="30"
      >
        <path
          d="M476.16 211.84h128v128h-128zM476.16 448h128v128h-128zM476.16 684.16h128v128h-128z"
          fill="#231815"
          p-id="2011"
        />
      </svg>
    </span> 
  </div>
  <p class="text-grey-600 py-4">{{ content }}</p>
</template>
  
  <script setup>
   defineProps(["user", "avatar", "time", "content"]);
  </script>
  
  <style scoped>
  
  </style>