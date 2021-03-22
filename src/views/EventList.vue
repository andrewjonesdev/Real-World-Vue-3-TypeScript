<template>
  <h1>Events for Good</h1>
  <div class="events">
    <EventCard v-for="event in events.events" :key="event.id" :event="event" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { EventList } from '@/types'

import EventCard from '../components/EventCard.vue'
import EventService from '../services/EventService'
//import EventList from './EventList.vue'

export default defineComponent({
  name: 'EventList',
  components: {
    EventCard
  },
  data() {
    return {
      events: {} as EventList
    }
  },
  created() {
    EventService.getEvents()
      .then(response => {
        this.events = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
})
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
