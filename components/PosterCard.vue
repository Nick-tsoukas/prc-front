<template>
  <div>
    <!-- if band has logo then will render it else will default to prc background  -->
    <div
      class="w-full sm:w-[432px] h-auto pb-[16px] border-4 border-main-red"
      :style="[
        band.logo
          ? { background: `url(${band.logo.url})` }
          : { background: 'url(/punk-background.png)' },
      ]"
    >
      <!-- header of card -->
      <div class="h-[58px] w-full bg-black flex items-center justify-center">
        <NuxtLink :to="{ path: '/bandprofile', query: { band: band.id } }">
          <p
            v-if="band.bandName"
            class="chedder text-center card_header_size text-white m-0"
            style="text-decoration: underline"
          >
            <!-- add band.bandName -->
            {{ band.bandName }}
          </p>
        </NuxtLink>
      </div>
      <!-- end header of card -->
      <!-- innder container for card info -->
      <section class="p-[16px]">
        <!-- basic info component -->
        <section class="flex gap-[16px]">
          <div
            class="w-[238px] h-[160px] border-4 p-[16px] border-black bg-white flex flex-col justify-center"
          >
            <p v-if="band.genre" class="card_basic_info_text chedder">
              Punk/{{ band.genre }}
            </p>
            <p v-if="band.gereAlt" class="card_basic_info_text chedder">
              Punk/{{ band.genreAlt }}
            </p>
            <p
              v-if="band.city && band.state"
              class="card_basic_info_text chedder"
            >
              {{ band.city }}, {{ band.state }}
            </p>
            <p v-if="band.dateStarted" class="card_basic_info_text chedder">
              {{ band.dateStarted }}
            </p>
            <p class="card_basic_info_text chedder">555-555-5555</p>
          </div>
          <!-- secondary info box -->
          <div
            class="w-[144px] h-[160px] border-4 p-[16px] border-black bg-white flex flex-col justify-center"
          >
            <NuxtLink
              :to="{
                path: '/bandprofile',
                hash: '#showz',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">Showz</p>
            </NuxtLink>
            <NuxtLink
              :to="{
                path: '/tours',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">Tour</p>
            </NuxtLink>
            <NuxtLink
              :to="{
                path: '/classifieds',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">
                Classified
              </p>
            </NuxtLink>
            <NuxtLink
              :to="{
                path: '/bandprofile',
                hash: '#releases',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">
                Releases
              </p>
            </NuxtLink>
            <NuxtLink
              :to="{
                path: '/bandprofile',
                hash: '#songs',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">Songs</p>
            </NuxtLink>
            <NuxtLink
              :to="{
                path: '/bandprofile',
                hash: '#posts',
                query: { band: band.id },
              }"
            >
              <p class="text-[16px] chedder underline text-main-red">
                Chat Room
              </p>
            </NuxtLink>
          </div>
        </section>
        <!-- end of basic info component -->
        <!-- Logo Box and Add Box -->
        <section class="flex gap-[16px] mt-[16px]">
          <!-- logo -->

          <div v-if="band.logo" class="h-[240px] w-[240px]">
            <NuxtLink :to="{ path: '/bandprofile', query: { band: band.id } }">
              <img
                class="object-cover w-full h-full border-4 border-black hover:scale-110 transition-all duration-100"
                :src="band.logo.url"
                alt=""
              />
            </NuxtLink>
          </div>
          <div v-else class="h-[240px] w-[240px]">
            <NuxtLink :to="{ path: '/bandprofile', query: { band: band.id } }">
              <img
                class="object-cover w-full h-full border-4 border-black hover:scale-110 transition-all duration-100"
                src="~/static/punk-background.png"
                alt=""
              />
            </NuxtLink>
          </div>
          <!-- addvertisement box -->
          <div class="h-[240px] w-[144px] border-4 border-main-red bg-white">
            <!-- create action to take user to create add page ... think  -->
            <p class="underline chedder card_basic_info_text text-center">
              Create Add
            </p>
          </div>
        </section>
        <!-- end of logo box and add box  -->
      </section>
      <!-- end basic info card -->
      <!-- annoucement card container -->
      <section class="pl-[16px] pr-[16px]">
        <!-- end of context -->
        <!-- this is the container of the content -->
        <div
          class="h-[187px] border-4 border-black p-[16px] bg-white flex flex-col justify-around"
        >
          <div v-if="announcement" class="flex items-center">
            <h2 class="text-[13px] grow">{{ announcement.title }}</h2>
            <div class="flex">
              <img
                v-if="index !== 0"
                src="~/static/left.svg"
                alt=""
                class="h-8"
                @click="back"
              />
              <img
                v-if="index !== announcements.length - 1"
                src="~/static/right.svg"
                alt=""
                class="h-8"
                @click="forward"
              />
            </div>
          </div>
          <div v-else>
            <h2 class="text-[13px]">Keep posted on upcoming announcements</h2>
          </div>

          <div v-if="announcement" class="flex gap-2">
            <div v-if="announcement.image" class="h-[72px] w-[72px] flex-grow">
              <img
                :src="announcement.image.url"
                alt=""
                class="object-fill h-full"
              />
            </div>
            <div v-else class="h-[72px] w-[72px] flex-grow">
              <img
                src="~/static/punk-background.png"
                alt=""
                class="object-fill h-full"
              />
            </div>
            <div class="w-10/12 flex items-center">
              <p class="text-[12px]">
                {{ announcement.text }}
              </p>
            </div>
          </div>

          <div v-else class="flex gap-2">
            <div class="h-[72px] w-[72px] flex-grow">
              <img
                src="~/static/punk-background.png"
                alt=""
                class="object-fill h-full"
              />
            </div>
            <div class="w-10/12 flex items-center">
              <p class="text-[12px]">There are no annoucements yet released</p>
            </div>
          </div>

          <div v-if="announcement" class="bg-black pt-2 pb-2">
            <NuxtLink
              :to="{
                path: 'announcement',
                query: {
                  profileId: band.id,
                  announcementId: announcement.id,
                  profileType: 'bands',
                  profileName: band.bandName,
                },
              }"
            >
              <p class="text-white text-center text-[13px]">
                View Announcement
              </p>
            </NuxtLink>
          </div>
        </div>
        <!-- end of context -->
        <!-- This is the end of content container thing   -->
      </section>
      <!-- action buttons  -->
      <section class="flex justify-around px-[16px] pt-[8px]">
        <Button text="Become Fanatic" @click.native="fav(band.id)" />
        <Button text="$ 1 Add" />
        <Button text="$ 3 Classified" />
        <Button text="Share" />
      </section>
      <section class="px-[16px] pt-[8px]">
        <NuxtLink :to="{ path: '/bandprofile', query: { band: band.id } }">
          <Button
            class="bg-main-red chedder text-lg"
            text="View Profile"
            @click="logit"
          />
        </NuxtLink>
      </section>
    </div>
    <section
      v-if="errorMessage"
      class="w-screen h-full fixed top-0 right-0 flex items-center justify-center bg-black opacity-50 z-40"
      @click="close"
    ></section>
    <div
      v-if="errorMessage"
      class="w-[25%] h-[25%] fixed top-[45%] right-[38%] flex flex-col justify-center items-center bg-white z-50"
    >
      <h2 class="text-xl text-black">{{ errorMessage }}</h2>
      <Button text="Sign Up" />
      <Button text="Log In" />
      <div class="absolute top-2 right-2 cursor-pointer" @click="close">
        Close <span class="text-2xl">x</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    band: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  data() {
    return {
      errorMessage: '',
      userFavs: [],
      updated: null,
      index: 0,
    }
  },

  computed: {
    announcement() {
      return this.band.announcements[this.index] || ''
    },
    announcements() {
      return this.band.announcements || ''
    },
  },

  methods: {
    logit() {
      console.log('hey this is a double click')
    },
    async fav(bandId) {
      const stringId = bandId.toString()
      console.log(stringId)
      if (!this.$strapi.user) {
        this.errorMessage = 'You have to be logged in to your favorites '
      } else {
        // get all user favorite stuff ... if they have any ... add a new favorite to it ... then resave all favoites to the user favs then route to favorite page the userFavs is an array so you can iterate over it using an array method wich is really an object at the end of the day or it wouldn't be about to have a method attached to it. Thank you for coming ... please come again soon.
        const user = await this.$strapi.user
        this.userFavs = await user.favs
        const json = { favObject: { type: 'band', id: stringId } }
        this.userFavs.push(json)
        //  favs: [...this.userFavs, { favObject: { ...json } }],
        console.log(this.userFavs)
        try {
          const f = await this.$strapi.update('users', this.$strapi.user.id, {
            favs: this.userFavs,
          })

          console.log(f)
        } catch (error) {
          this.errorMesage = 'error'
          console.log(error, 'this is the error message')
        }
      }

      this.$router.push({
        path: 'favorites',
        query: { user: this.$strapi.user.id, favs: this.updated },
      })
    },
    close() {
      this.errorMessage = ''
    },
    forward() {
      if (this.index !== this.announcements.length - 1) {
        this.index++
      }
    },
    back() {
      if (this.index !== 0) {
        this.index--
      }
    },
  },
}
</script>

<style scoped>
.card_header_size {
  font-size: 56px;
}
.card_basic_info_text {
  font-size: 27px;
}
</style>
