<template>
  <div class="chat-container">
    <div class="chat-header">
      <h2>Chat</h2>
    </div>
    <div class="chat-body" ref="chatBody">
      <div
        v-for="(message, index) in messages"
        :key="index"
        :class="message.type"
        class="message"
      >
        <div v-if="message.type === 'user'" class="message-content user">
          <p>{{ message.text }}</p>
        </div>
        <div v-if="message.type === 'bot'" class="message-content bot">
          <p>{{ message.text }}</p>
        </div>
      </div>
    </div>
    <div class="chat-footer">
      <textarea 
        v-model="userMessage" 
        @keyup.enter="sendMessage" 
        placeholder="Type your message here..." />
      <button @click="sendMessage" class="send-btn">Send</button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  msg: String
});

const userMessage = ref("");
const messages = ref([]);

const sendMessage = () => {
  if (userMessage.value.trim()) {
    messages.value.push({ type: "user", text: userMessage.value });
    const msg = userMessage.value;
    userMessage.value = "";
    messages.value.push({
        type: "bot",
        text: "...",
      });

    setTimeout(() => {
      messages.value.pop();
      messages.value.push({
        type: "bot",
        text: `You said: "${msg}"`,
      });
    }, 1000);
  }
};

watch(() => props.msg, (newVal) => {
  if (newVal) {
    userMessage.value = newVal;
    sendMessage();
  }
},{
  immediate: true
}
);

</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f3f3f3;
}

.chat-container {
  width: 50%;
  background-color: whitesmoke;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  border: 1px solid #ccc;
  display: flex;
  flex-direction: column;
  height: 90vh;
  overflow: hidden;
}

.chat-header {
  background-color: seagreen;
  padding: 10px;
  color: white;
  text-align: center;
  font-size: 18px;
  font-weight: bold;
}

.chat-body {
  flex-grow: 1;
  padding: 10px;
  overflow-y: auto;
}

.message {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}

.message-content {
  max-width: 80%;
  padding: 8px;
  border-radius: 5px;
  font-size: 14px;
  word-wrap: break-word;
  line-height: 1.5;
}

.message.user .message-content {
  background-color: #f1f1f1;
  align-self: flex-end;
}

.message.bot .message-content {
  background-color: #e0f7fa;
  align-self: flex-start;
}

.chat-footer {
  display: flex;
  padding: 10px;
  background-color: #ebebeb;
  display: flex;
  align-items: center;
}

.message-input {
  flex-grow: 1;
  padding: 8px;
  border-radius: 20px;
  border: 1px solid #ccc;
  font-size: 14px;
}

.send-btn {
  background-color: seagreen;
  color: white;
  border: none;
  padding: 8px 15px;
  border-radius: 20px;
  cursor: pointer;
  margin-left: 10px;
}

.send-btn:hover {
  background-color: #45a049;
}

.chat-footer input:focus {
  outline: none;
  border-color: #4caf50;
}

textarea {
  height: 100px;
  padding: 10px;
  margin-top: 20px;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ddd;
  resize: none;
  flex-grow: 1;

}
  
textarea:focus {
  outline: none;
}
</style>
