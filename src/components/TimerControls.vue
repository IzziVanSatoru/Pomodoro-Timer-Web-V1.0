<template>
  <div class="d-flex justify-content-center gap-3">
    <button
      class="btn"
      :class="!isRunning ? 'btn-success' : 'btn-secondary'"
      @click="$emit('start')"
      :disabled="isRunning"
    >
      ▶ Start
    </button>

    <button
      class="btn btn-warning"
      @click="$emit('pause')"
      :disabled="!isRunning"
    >
      ⏸ Pause
    </button>

    <button
      class="btn btn-danger"
      @click="$emit('reset')"
    >
      🔄 Reset
    </button>
  </div>
</template>

<script setup>
defineProps({
  isRunning: Boolean
})
</script>
