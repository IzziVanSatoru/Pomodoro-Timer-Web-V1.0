<template>
  <div class="p-3" style="text-align: center; background-color: #fffef6cc; border-radius: 16px;">
    <h2 style="font-weight: bold; font-size: 1.8rem; margin-bottom: 16px; color: #2c2c2c;">
      🌸 Pomodoro Timer
    </h2>

    <div class="mb-3">
      <label style="font-size: 0.95rem; color: #555;">
        Set Duration (minutes): 
        <input
          type="number"
          v-model.number="inputMinutes"
          :disabled="isRunning"
          min="1"
          style="width: 80px; padding: 6px; font-size: 1rem; border-radius: 8px; border: 1px solid #ccc;"
        />
      </label>
    </div>

    <div
      style="font-size: 3.2rem; font-family: 'Courier New', monospace; color: #333; padding: 10px;"
    >
      {{ formattedTime }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch, onUnmounted } from 'vue'
import { supabase } from '../composables/useSupabase.js'

const inputMinutes = ref(25)
const time = ref(inputMinutes.value * 60)
const isRunning = ref(false)
let interval = null

watch(inputMinutes, (val) => {
  if (!isRunning.value) {
    time.value = val * 60
  }
})

const formattedTime = computed(() => {
  const m = String(Math.floor(time.value / 60)).padStart(2, '0')
  const s = String(time.value % 60).padStart(2, '0')
  return `${m}:${s}`
})

function startTimer() {
  if (isRunning.value) return
  isRunning.value = true
  interval = setInterval(() => {
    if (time.value > 0) {
      time.value--
    } else {
      clearInterval(interval)
      isRunning.value = false
      saveSession(inputMinutes.value)
      alert('Pomodoro selesai! Disimpan ke histori.')
    }
  }, 1000)
}

function pauseTimer() {
  clearInterval(interval)
  isRunning.value = false
}

function resetTimer() {
  pauseTimer()
  time.value = inputMinutes.value * 60
}

async function saveSession(minutes) {
  await supabase.from('study_sessions').insert([
    { duration_min: minutes, note: 'Pomodoro selesai dari input' }
  ])
}

onUnmounted(() => clearInterval(interval))

defineExpose({ startTimer, pauseTimer, resetTimer, isRunning })
</script>
