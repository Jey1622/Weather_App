<template>
  <v-app>
    <v-main>
      <weather-app/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import WeatherApp from './components/WeatherApp.vue'

export default {
  name: 'App',

  components: {

    WeatherApp,
  },

  data: () => ({
    //
  }),
}
</script>
