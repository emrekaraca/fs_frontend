<template>
  <div>
    <h1>Etkinlikler</h1>
    <br>
    <template v-for="(calendarEvent, index) in events">
      <calendar-entry
        :calendar-event="calendarEvent"
        :key="index"
      />
    </template>
  </div>
</template>

<script>
import CalendarEntry from './CalendarEntry'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()

export default {
  components: {
    CalendarEntry
  },
  asyncData({ env }) {
    return Promise.all([
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'event',
        order: 'fields.startDate'
      })
    ])
      .then(([events]) => {
        // return data that should be available
        // in the template
        return {
          events: events.items
        }
      })
      .catch(console.error)
  }
}
</script>

<style lang="scss" scoped>
</style>
