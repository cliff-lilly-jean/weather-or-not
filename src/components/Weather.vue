<template>
  <div id="weather">
    <div class="weather-card">
      <City :city="city"></City>
      <WeatherIcon :icon="icon"></WeatherIcon>
      <WeatherDescription
        :weatherDescription="weatherDescription"
      ></WeatherDescription>
      <Temperature
        :temp="temp"
        :humidity="humidity"
        :windSpeed="windSpeed"
      ></Temperature>
    </div>
  </div>
</template>

<script>
import Temperature from "./Temperature";
import WeatherDescription from "./weatherDescription";
import WeatherIcon from "./WeatherIcon";
import City from "./City";
export default {
  components: { Temperature, WeatherDescription, WeatherIcon, City },
  props: [
    "weatherDescription",
    "temp",
    "icon",
    "humidity",
    "windSpeed",
    "city",
  ],
  methods: {
    // Create a method to query the api
  },
};
</script>

<style scoped>
.weather-card {
  background: rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(8.5px);
  -webkit-backdrop-filter: blur(8.5px);
  border-radius: 10px;
  max-width: 500px;
  margin: 0 auto;
  padding: 50px;
}
</style>