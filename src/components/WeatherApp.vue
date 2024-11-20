<template>
  <v-app>
    <v-container>
      <v-card
        class="mx-auto pa-4"
        max-width="600"
        :class="{ 'warm-bg': state_weather ,'default':!state_weather}"
      >
        <v-text-field
          label="Search city"
          v-model="data.city"
          placeholder="Search..."
          solo
          dense
          outlined
          @keyup.enter="getApi"
        ></v-text-field>

        <v-divider v-if="data.weather" class="my-4"></v-divider>

        <v-container v-if="data.weather">
          <v-row>
            <v-col class="text-center">
              <h1>{{ data.weather.name }}</h1>
              <h3>{{ new Date().toLocaleString() }}</h3>
            </v-col>
          </v-row>

          <v-row justify="center" class="my-4">
            <v-col class="text-center">
              <v-card class="d-inline-block pa-5 text-center" elevation="5">
                <h2 class="display-3">
                  {{ Math.round(data.weather.main.temp) }}&deg;
                </h2>
              </v-card>
            </v-col>
          </v-row>

          <v-row justify="center">
            <v-col class="text-center">
              <h3>{{ data.weather.weather[0].main }}</h3>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-container>
  </v-app>
</template>
  
  <script>
import axios from "axios";

export default {
  name: "WeatherApp",
  data() {
    return {
      data: {
        city: "",
        weather: null,
      },
      state_weather: false,
    };
  },
  mounted: async function () {
    this.getApi();
  },
  methods: {
    async getApi() {
      if (this.data.city === "") {
        this.data.city = "chennai";
      }
      const getWeather = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?units=metric&q=${this.data.city}&appid=261514ec6ead072a338a344dce0fb58f`
      );
      this.data.weather = getWeather.data;
      this.data.city = "";
      this.state_weather = this.data.weather.main.temp > 16;
    },
  },
};
</script>
  
  <style scoped>
.warm-bg {
  background: linear-gradient(
    to bottom,
    rgba(248, 8, 8, 0.35),
    rgba(246, 6, 6, 0.75)
  );
  color: white;
}
.default{
    background: linear-gradient(
    to bottom,
    rgba(8, 172, 248, 0.35),
    rgba(6, 114, 246, 0.75)
  );
  color: white;
}
</style>
  