<template>
  <article class="grid grid-cols-3 w-[100vw] h-[100vh]">
    <section>
      <h1>Digite seu nome:</h1>
      <input type="text" class="bg-blue-200 rounded-xl w-[80%] pl-3" v-model="username">
    </section>
    <section class="col-span-2  flex flex-col justify-between py-5 items-center">
     <div>
      <h1 class="text-2xl">CHAT - TEFLY<span class="text-[#00000070] text-[15px]">(teste)</span></h1>
     </div>
      <Chat :messages="messages" v-show="messages.length > 0" :author="username"/>
      <div class="flex gap-3 w-[100%]">
        <input type="text" class="bg-blue-200 rounded-xl w-[80%] pl-3" v-model="msg">
        <button class="bg-blue-500 rounded-xl w-[50px] h-[50px] flex items-center justify-center" @click="sendMessage"><img src="./assets/send.svg" alt="" class="w-[30px] h-[30px]"></button>
      </div>
    </section>
  </article>
</template>

<script>
import Chat from './components/Chat.vue'
import {io} from 'socket.io-client';

export default {
  name: 'App',
  created(){
    this.socket = io('http://localhost:8081')
    this.socket.on('newmsg',(data)=>{
      this.messages.push(data)
    } )
  },
  data(){
    return{
      username: '',
      msg:'',
      messages: []
    }
  },
  components: {
    Chat
  },
  methods:{
    sendMessage: function(){
      if(this.username != ''){
        this.socket.emit('msg', {msg:this.msg, username: this.username})
      }
    }
  }
}
</script>