<template>
  <div v-if="events">
    <h1 class="text-5xl text-center main_red_text my-6">Showz</h1>
    <section class="container mx-auto">
      <div
        v-for="(event, index) in events"
        :key="events.title + index"
        class="shadow-md w-full h-full flex flex-col ms:h-64 sm:my-12 sm:mx-auto sm:flex-row transition-all duration-200 hover:scale-105"
      >
        <div v-if="event.eventPoster" class="w-full sm:w-1/3 h-64">
          <img
            class="h-full w-full object-cover"
            :src="event.eventPoster.url"
            alt=""
          />
        </div>
        <div class="p-6">
          <p class="chedder text-xl inline sm:text-center sm:block">
            {{ moment(String(event.date)).format('MMM') }}
          </p>
          <p class="chedder text-xl inline sm:text-center sm:block">
            {{ moment(String(event.date)).format('Do') }}
          </p>
        </div>
        <div class="flex flex-col flex-grow p-6">
          <div>
            <p v-if="event.title" class="chedder text-2xl">
              {{ event.title }}
            </p>
            <p v-if="event.headlinerOne" class="text-xl font-black pb-2">
              Featuring {{ event.headlinerOne }}
            </p>
            <p v-if="event.streetAddress && event.streetName" class="text-xl">
              The Vic, {{ event.streetAddress }} {{ event.streetName }} /
              {{ moment(String(event.date)).format('LT') }} -
              {{ moment(event.timeEnds, 'h').format('LT') }}
            </p>
            <p v-if="event.city && event.state" class="text-xl">
              {{ event.city }}, {{ event.state }}
            </p>
          </div>
          <div class="flex-grow flex items-center my-4 sm:my-0">
            <NuxtLink
              :to="{ path: 'eventview', query: { event: event.id } }"
              class="border-2 border-black px-4 py-2"
              >View Event</NuxtLink
            >
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  data() {
    return {
      events: '',
    }
  },
  async mounted() {
    const events = await this.$strapi.find('events')
    this.events = events
  },

  methods: {
    moment,
  },
}
</script>

<style lang="scss" scoped></style>
