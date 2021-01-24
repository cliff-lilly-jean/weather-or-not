<template>
  <div id="bkg">
    <Weather
      :weatherDescription="weatherDescription"
      :temp="temp"
      :icon="icon"
      :humidity="humidity"
      :windSpeed="windSpeed"
      :city="city"
    ></Weather>
  </div>
</template>

<script>
import Weather from "./Weather";
export default {
  props: [
    "weatherDescription",
    "temp",
    "icon",
    "humidity",
    "windSpeed",
    "city",
  ],
  components: {
    Weather,
  },
};
</script>

<style>
</style>