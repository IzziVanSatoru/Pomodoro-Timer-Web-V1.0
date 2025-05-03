<template>
  <div style="margin-top: 30px;">
    <h2>Study History</h2>
    <p v-if="loading">Loading...</p>
    <ul v-else>
      <li v-for="s in history" :key="s.id">
        {{ s.duration_min }} mins — {{ formatDate(s.created_at) }} — {{ s.note || '' }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../composables/useSupabase.js'

const history = ref([])
const loading = ref(true)

onMounted(async () => {
  const { data } = await supabase
    .from('study_sessions')
    .select('*')
    .order('created_at', { ascending: false })

  history.value = data
  loading.value = false
})

function formatDate(d) {
  return new Date(d).toLocaleString()
}
</script>
