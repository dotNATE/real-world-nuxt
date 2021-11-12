<template>
  <div>
    <h1>Events</h1>

    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventService from '@/services/EventService'
import EventCard from '@/components/EventCard.vue'

export default {
  components: {
    EventCard,
  },
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents()

      return {
        events: data,
      }
    } catch {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again later.',
      })
    }
  },
  head: {
    title: 'Create an Event',
  },
}
</script>
