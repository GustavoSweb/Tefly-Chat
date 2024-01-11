<template>
  <div class="w-[100%] h-[80vh] overflow-y-scroll pb-[50px]">
    <div
      v-for="message in messages"
      :key="message.msg + Date.now()"
      class="w-[80%]"
    >
      <div class="flex w-[100%] justify-end" v-if="author == message.username">
        <div
          
          class="bg-blue-500 p-2 pr-5 text-white rounded-xl w-min min-w-[150px] max-w-[300px] mt-4"
        >
          <p class="break-words">{{ message.msg }}</p>
        </div>
      </div>
      <div class="flex w-[100%] justify-start" v-else>
        <div
          
          class="bg-white shadow-lg p-2 pr-5 text-black rounded-xl min-w-[150px] max-w-[300px]  mt-4"
        >
        <small class="text-[#00000070] mb-3">{{ message.username }}</small>
          <p class=" break-words">{{ message.msg }}</p>
        </div>
      </div>
  </div>
  </div>
</template>

<script>
export default {
  name: "Chat-Component",
  props: {
    messages: Array,
    author: String,
  },
};
</script>
