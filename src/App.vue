<script setup lang="ts">
import Editor from './components/Editor.vue';
import Chat from './components/Chat.vue';
import HomePage from './components/HomePage.vue';
import { ref } from 'vue';

const msg = ref('');

function onChat(text: string) {
  msg.value = text;
}

</script>

<template>
  <div v-if="!msg">
    <HomePage @on-chat="onChat"/>
  </div>
  <div v-else class="chatCl">
    <Chat :msg="msg"/>
    <Editor/>
  </div>
</template>

<style scoped>
.chatCl {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 25px;
  overflow: hidden;
}
</style>
