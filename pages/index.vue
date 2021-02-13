<template>
  <div>
    <h1>Events</h1>

    <event-card
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    ></event-card>
  </div>
</template>

<script>
import EventCard from '../components/EventCard.vue'
export default {
  components: { EventCard },
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get(
        'https://my-json-server.typicode.com/Hrach-1/real-world-nuxt/events'
      )

      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  }
}
</script>
