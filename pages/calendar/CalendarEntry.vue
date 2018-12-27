<template>
  <div class="calendar-entry-outer-container">
    <h3>{{ calendarEvent.fields.title }}</h3>
    <p>Başlangıç: {{ calendarEvent.fields.startDate.slice(0,10) }}</p>
    <p>Bitiş: {{ calendarEvent.fields.endDate.slice(0,10) }}</p>
    <div v-html="docToString(calendarEvent.fields.text)" />
    <p>Eğitmen: {{ calendarEvent.fields.speaker[0].fields.firstName }} {{ calendarEvent.fields.speaker[0].fields.lastName }}</p>
    <p>Mekan: {{ calendarEvent.fields.information }}</p>
    <p>Yer: {{ calendarEvent.fields.location }}</p>
    <p>Fiyat: {{ calendarEvent.fields.price }}</p>
    <br>
  </div>
</template>

<script>
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
export default {
  props: {
    calendarEvent: {
      default() {
        return null
      },
      type: Object
    }
  },
  methods: {
    docToString(input) {
      return documentToHtmlString(input)
    }
  }
}
</script>

<style lang="scss" scoped>
.calendar-entry-outer-container {
  border: 1px dashed grey;
  padding: 20px;
  width: 1100px;
  margin: 20px 0;
}
</style>
