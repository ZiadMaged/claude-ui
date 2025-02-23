<template setup>
  <div>
    <div ref="mermaidContainer" class="mermaid">
      flowchart TD;
        A[Christmas] -->|Get money| B(Go shopping);
        B --> C{Let me think};
        C -->|One| D[Laptop];
        C -->|Two| E[iPhone];
        C -->|Three| F[fa:fa-car Car];
  
    </div>
  </div>
</template>

<script setup>
import mermaid from 'mermaid';
import { onMounted, ref } from 'vue';

const mermaidContainer = ref(null);

onMounted(() => {
  if (mermaidContainer.value) {
    mermaid.initialize({ startOnLoad: true });
    mermaid.contentLoaded();
  }
});
</script>

<style scoped>
.mermaid {
  width: 100%;
  height: 80vh;
}
</style>
