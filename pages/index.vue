<template>
  <div>
    <div class="hidden xl:block"><HeroAlt /></div>
    <div class="block xl:hidden"><Hero /></div>

    <section>
      <h2 class="text-center my-10 text-5xl">Featured Bands</h2>
      <div
        v-if="bands !== []"
        class="flex flex-col w-[80%] mx-auto xl:flex-row xl:w-auto justify-center gap-14"
      >
        <!-- <BandCard
          v-for="(band, index) in bands.slice(0, 3)"
          :key="band.bandName + index"
          :band="band"
          :isFeatured="true"
          style="min-width: 25vw"
        /> -->

        <PosterCard
          v-for="(band, index) in bands.slice(0, 3)"
          :key="band.bandName + index"
          :band="band"
          :isFeatured="true"
          style="min-width: 25vw"
          class="hover:scale-110 transition-all duration-100"
          @dblclick="console.log('hello')"
        />
      </div>
    </section>
    <!-- this describes the pricing model  -->
    <!-- <Price /> -->
    <!-- <section>
      <h2 class="text-center my-10 text-5xl">All bands</h2>
      <SliderContainer v-if="bands !== []">
        <PosterCard
          v-for="(band, index) in bands"
          :key="band.bandName + index"
          :band="band"
          :isFeatured="true"
          style="min-width: 25vw"
        />
      </SliderContainer>
    </section> -->

    <section class="my-10">
      <h2 class="chedder text-center text-5xl">Featured Event</h2>
      <FeaturedEvent v-if="event" :event="event" />
    </section>
    <section class="my-10">
      <Cta />
    </section>
    <section class="my-10">
      <Gallery />
    </section>
    <section>
      <NewsLetterCta />
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bands: [],
      event: null,
    }
  },
  async mounted() {
    try {
      this.bands = await this.$strapi.find('bands')
      this.event = await this.$strapi.find('featured-event')
    } catch (error) {
      return error
    }
  },
}
</script>
