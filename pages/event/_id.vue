<template>
  <h1>{{ event.title }}</h1>
</template>

<script>
import EventService from '@/services/EventService'

export default {
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)

      return {
        event: data,
      }
    } catch {
      error({
        statusCode: 503,
        message: 'Unable to fetch Event #' + params.id,
      })
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'at you need to know about Event #' + this.event.title,
        },
      ],
    }
  },
}
</script>