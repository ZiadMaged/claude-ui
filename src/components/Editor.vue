<template>
  <div class="editor">
    <div class="bar">
        <p>{{isCode ? 'Code' : 'Diagram'}}</p>
        <div @click="isCode = !isCode">
          <div class="toggle-switch" :class="{ 'active': isCode}">
            <div class="toggle-button" :class="{ 'move': isCode }"></div>
          </div>
        </div>
    </div>
    
    <div class="codemirror">
      <codemirror
        v-if="isCode"
        v-model="code"
        :options="editorOptions"
        :style="{ width: '100%', height: '100%' }"
      />
      <FlowchartConverter v-else/>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Codemirror } from 'vue-codemirror'
import FlowchartConverter from './FlowchartConverter.vue';

const code = ref(`const greet = (name) => {
  return \`Hello, \${name}!\`;
};

console.log(greet('Vue Developer'));
`)

const editorOptions = ref({
  mode: 'javascript',
  theme: 'dracula',
  lineNumbers: true,
  tabSize: 2,
  indentUnit: 2,
  lineWrapping: true,
})

const isCode = ref(false);

function onSwitch() {
  isCode.value = !isCode.value;
}

</script>

<style scoped>
.codemirror {
  border: 1px solid #ccc;
  background-color: whitesmoke;
  height: 84vh;
}

.toggle{
  background-color: seagreen;
  color: white;
}

.bar{
  background-color: #ebebeb;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  padding-left: 10px;
  padding-right: 10px;
}

.editor {
  width: 50%;
  box-shadow:0 4px 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  height: 90vh;
  overflow: hidden;
}

/* Container that holds the toggle */
.toggle-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

/* The outer toggle switch background */
.toggle-switch {
  width: 4rem; /* Equivalent to w-16 */
  height: 1rem; /* Equivalent to h-10 */
  display: flex;
  align-items: center;
  background-color: #d1d5db; /* Equivalent to bg-gray-300 */
  border-radius: 9999px; /* Equivalent to rounded-full */
  padding: 0.25rem; /* Equivalent to p-1 */
  transition: background-color 0.3s ease-in-out; /* Equivalent to duration-300 ease-in-out */
}

/* When toggle is active (green background) */
.toggle-switch.active {
  background-color: seagreen; /* Equivalent to bg-green-400 */
}

/* The button inside the switch */
.toggle-button {
  background-color: white;
  width: 1.5rem; /* Equivalent to w-8 */
  height: 1.5rem; /* Equivalent to h-8 */
  border-radius: 50%; /* Equivalent to rounded-full */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Equivalent to shadow-md */
  transition: transform 0.1s ease-in-out; /* Equivalent to duration-300 ease-in-out */
}

/* When toggle is active (button moves right) */
.toggle-button.move {
  transform: translateX(3rem); /* Equivalent to translate-x-6 */
}

</style>