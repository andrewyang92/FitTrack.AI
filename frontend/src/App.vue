<template>
  <main style="font-family: ui-sans-serif, system-ui; padding: 2rem">
    <h1>FitTrack.AI</h1>
    <p>Vue 前端已啟動。</p>
    <button @click="check" style="padding: .5rem 1rem; margin:.5rem 0;">測試後端健康檢查</button>
    <pre v-if="result" style="background:#111; color:#0f0; padding:1rem; border-radius:.5rem; overflow:auto;">{{ result }}</pre>
  </main>
</template>

<script setup>
import { ref } from 'vue'
const result = ref('')
async function check() {
  try {
    const base = import.meta.env.VITE_API_BASE || 'http://localhost:8000'
    const res = await fetch(base + '/health')
    result.value = JSON.stringify(await res.json(), null, 2)
  } catch (e) {
    result.value = String(e)
  }
}
</script>
