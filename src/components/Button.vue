<template>
  <button @click="goToHistory" class="btn btn-outline-primary">
    📚 Lihat Riwayat Belajar
  </button>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

function goToHistory() {
  router.push('/history')
}
</script>
