<template>
    <div class="prompt-area">
        <h1>What can I help with?</h1>
        <textarea 
            v-model="prompt" 
            @keyup.enter="sendPrompt" 
            placeholder="Type your message here..." />
        <button @click="sendPrompt">Send</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const prompt = ref('');

const emits = defineEmits(["on-chat"]);


const sendPrompt = () => {
    if (prompt.value.trim()) {
        emits('on-chat', prompt.value);
        prompt.value = '';
    }
};
</script>

<style scoped>
.app-container {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f9f9f9;
    padding: 20px;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
}

header .logo {
    font-weight: bold;
    font-size: 24px;
    color: #333;
}

header nav a {
    margin: 0 10px;
    text-decoration: none;
    color: #555;
}

main {
    margin-top: 50px;
}

.prompt-area {
    display: flex;
    flex-direction: column;
    align-items: center;
}

textarea {
    width: 50%;
    height: 100px;
    padding: 10px;
    margin-top: 20px;
    font-size: 16px;
    border-radius: 8px;
    border: 1px solid #ddd;
    resize: none;
}

textarea:focus {
    outline: none;
}

button {
    margin-top: 15px;
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

footer {
    margin-top: 50px;
    font-size: 14px;
    color: #777;
}
</style>