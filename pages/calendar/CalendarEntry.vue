<template>
  <div class="calendar-entry-outer-container">
    <h3>{{ calendarEvent.fields.title }}</h3>
    <p>Başlangıç: {{ calendarEvent.fields.startDate.slice(0,10) }}</p>
    <p>Bitiş: {{ calendarEvent.fields.endDate.slice(0,10) }}</p>
    <div v-html="docToString(calendarEvent.fields.text)" />
    <p>Eğitmen: {{ calendarEvent.fields.speaker[0].fields.firstName }} {{ calendarEvent.fields.speaker[0].fields.lastName }}</p>
    <p v-if="calendarEvent.fields.information">Bilgi ve Başvuru: {{ calendarEvent.fields.information }}</p>
    <p v-if="calendarEvent.fields.location">Yer: {{ calendarEvent.fields.location }}</p>
    <p v-if="calendarEvent.fields.price">Fiyat: {{ calendarEvent.fields.price }}</p>
    <p v-if="calendarEvent.fields.fbLink">Facebook Link: {{ calendarEvent.fields.fbLink }}</p>
    <p v-if="calendarEvent.fields.links">Diğer Linkler: {{ calendarEvent.fields.links.join("\n") }}</p>
    <p v-if="calendarEvent.fields.course">Akademi bağlantısı: {{ calendarEvent.fields.course.fields.title }}</p>
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
