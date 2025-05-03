<template>
  <div class="container py-5" style="max-width: 700px; font-family: 'Noto Sans JP', sans-serif;">
    <div class="text-center mb-5">
      <h1 class="fw-bold" style="font-size: 2.5rem; color: #2d2d2d;">🍃 Pomodoro Timer</h1>
      <p style="color: #666; font-size: 1rem;">Focus gently. One breath, one task at a time.</p>
    </div>

    <div class="shadow p-4 rounded-4 border" style="background-color: #ffffffcc;">
      <PomodoroTimer ref="timer" />

      <div class="d-flex justify-content-center gap-3 my-4">
        <TimerControls
          :isRunning="isRunning"
          @start="startTimer"
          @pause="pauseTimer"
          @reset="resetTimer"
        />
      </div>

      <div class="text-end">
        <Button />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import PomodoroTimer from '../components/PomodoroTimer.vue'
import TimerControls from '../components/TimerControls.vue'
import Button from '../components/Button.vue'

const timer = ref(null)
const isRunning = ref(false)

function startTimer() {
  isRunning.value = true
  timer.value?.startTimer()
}

function pauseTimer() {
  isRunning.value = false
  timer.value?.pauseTimer()
}

function resetTimer() {
  isRunning.value = false
  timer.value?.resetTimer()
}
</script>
