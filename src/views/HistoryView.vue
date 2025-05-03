<template>
  <div class="container py-5" style="max-width: 800px; font-family: 'Noto Sans JP', sans-serif;">
    <div class="text-center mb-4">
      <h1 class="fw-bold" style="font-size: 2rem; color: #2c2c2c;">📖 Study History</h1>
      <p style="color: #555;">Your recent focus sessions</p>
    </div>

    <!-- Tombol Back -->
    <div class="mb-4">
      <button @click="goBack" class="btn btn-outline-secondary">
        ← Back to Home
      </button>
    </div>

    <!-- Dashboard Riwayat -->
    <div v-if="loading" class="text-center">Loading...</div>

    <div v-else-if="history.length === 0" class="text-center text-muted">
      No history found.
    </div>

    <div v-else>
      <div
        v-for="item in history"
        :key="item.id"
        class="p-3 mb-3 border rounded-4 shadow-sm"
        style="background-color: #fefefecc;"
      >
        <p class="mb-1">
          <strong>🕒 Duration:</strong> {{ item.duration_min }} minutes
        </p>
        <p class="mb-1">
          <strong>📅 Time:</strong> {{ formatDate(item.created_at) }}
        </p>
        <p v-if="item.note" class="mb-0 fst-italic">
          “{{ item.note }}”
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import { supabase } from '../composables/useSupabase.js'

const router = useRouter()
const history = ref([])
const loading = ref(true)

function goBack() {
  router.push('/')
}

onMounted(async () => {
  const { data, error } = await supabase
    .from('study_sessions')
    .select('*')
    .order('created_at', { ascending: false })

  if (error) {
    console.error(error.message)
  }

  history.value = data || []
  loading.value = false
})

function formatDate(date) {
  return new Date(date).toLocaleString()
}
</script>
