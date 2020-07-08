<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input
        v-model="search"
        placehoder="Search"
        borderless
        dark
      >
        <template v-slot:before>
          <q-icon
            name="my_location"
            @click="getLocation"
          />
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>

    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          Manchester
        </div>
        <div class="text-h6 text-weight-light">
          Rain
        </div>
        <div class="text-h1 text-weight-thin relative-position">
          <span>8</span>
          <span class="text-h4 relative-position degree">&deg;</span>
        </div>
      </div>

      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100" alt="Bill" />
      </div>
    </template>

    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">
          Quasar Weather
        </div>
        <q-btn
          class="col"
          flat
          @click="getLocation"
        >
          <q-icon left size="3em" name="my_location" />
          <div>Find my location</div>
        </q-btn>
      </div>
    </template>

    <div class="col skyline" />
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  data: () => ({
    search: '',
    weatherData: null,
    lat: null,
    long: null
  }),

  methods: {
    getLocation() {
      navigator.geolocation.getCurrentPosition(position => {
        this.lat = position.coords.latitude;
        this.long = position.coords.longitude
      })
    }
  }
}
</script>

<style lang="sass" scoped>
  .q-page
    background: linear-gradient(to bottom, #136a8a, #267871)
  .degree
    top: -44px
  .skyline
    flex: 0 0 100px
    background-image: url('../statics/town_silhouette.png')
    background-size: contain
    background-position: center bottom
</style>