<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { RouterLink } from 'vue-router'

interface Event {
  id: number
  name: string
  place: string
  time: string
}

const events = ref<Event[]>([])

const fetchEvents = async () => {
  const response = await fetch('/api/events')
  const data = await response.json()
  events.value = data
}

onMounted(() => {
  fetchEvents()
})
</script>



<template>
  <main>
    Home

    <div>Pendaftaran pondok pesantren Alberr</div>
<div>
      <RouterLink to="/event">Buat Event</RouterLink>
    </div>
    <div>
      <ul>
        <li v-for="event in events" :key="event.id">
          <div>{{ event.name }}</div>
          <div>{{ event.place }}</div>
          <div>{{ new Date(Number(event.time) * 1000).toLocaleString() }}</div>
          <div>
            <RouterLink :to="`/event/${event.id}`">Edit</RouterLink>
          </div>
        </li>
      </ul>
    </div>
  </main>
</template>
