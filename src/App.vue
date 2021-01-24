<template>
  <div id="app">
    <WeatherBackground
      v-if="currentWeatherId >= 200 && currentWeatherId <= 299"
      :class="['thunderstorm', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId >= 300 && currentWeatherId <= 399"
      :class="['drizzle', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId >= 500 && currentWeatherId <= 599"
      :class="['rain', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId >= 600 && currentWeatherId <= 699"
      :class="['snow', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId >= 700 && currentWeatherId <= 799"
      :class="['atmosphere', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId == 800"
      :class="['clear', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
    <WeatherBackground
      v-else-if="currentWeatherId >= 801 && currentWeatherId <= 899"
      :class="['clouds', 'container']"
      :weatherDescription="currentWeatherDescription"
      :temp="currentTemperature"
      :icon="returnedIcon"
      :humidity="currentHumidity"
      :windSpeed="currentWeatherWindSpeed"
      :city="city"
    ></WeatherBackground>
  </div>
</template>

<script>
// API call: https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={API key}
// Google Maps API Key: AIzaSyDbDLtySKbZePECwNvxTaqzck57bN9NzA8
// https://maps.googleapis.com/maps/api/geocode/json?latlng=this.lattitude,this.longitude&key=AIzaSyDbDLtySKbZePECwNvxTaqzck57bN9NzA8
import WeatherBackground from "./components/WeatherBackground";
import axios from "axios";
export default {
  name: "App",
  components: {
    WeatherBackground,
  },
  data() {
    return {
      lattitude: "",
      longitude: "",
      currentTemperature: "",
      currentWeatherDescription: "",
      currentWeatherId: "",
      currentWeatherWindSpeed: "",
      currentHumidity: "",
      apiKey: process.env.VUE_APP_API_KEY,
      returnedIcon: "",
      city: "",
      // keys that correspond to the css classes for background images
      clear: "clear",
      thunderstorm: "thunderstorm",
      drizzle: "drizzle",
      rain: "rain",
      snow: "snow",
      atmosphere: "atmosphere",
      clouds: "clouds",
      container: "container",
    };
  },
  methods: {
    // Method to get the users location
    getUsersLocation(lat, long) {
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/onecall?lat=" +
            lat +
            "&lon=" +
            long +
            "&appid=" +
            this.apiKey +
            "&units=imperial"
        )
        .then((res) => {
          let descriptionReturn = res.data.current.weather[0].description.split(
            " "
          );
          let first = descriptionReturn[0];
          let last = descriptionReturn[1];

          descriptionReturn =
            first.charAt(0).toUpperCase() +
            first.substr(1) +
            " " +
            last.charAt(0).toUpperCase() +
            last.substr(1);

          // Response data
          this.currentWeatherDescription = descriptionReturn;
          this.currentWeatherId = res.data.current.weather[0].id;
          this.currentWeatherWindSpeed =
            Math.round(res.data.current.wind_speed) + "mph";
          this.returnedIcon = res.data.current.weather[0].icon;
          this.currentTemperature = Math.round(res.data.current.temp);
          this.currentHumidity = Math.round(res.data.current.humidity) + "%";
          console.log(res.data);
        });
    },
    getCity(lat, long) {
      axios
        .get(
          "https://maps.googleapis.com/maps/api/geocode/json?latlng=" +
            lat +
            "," +
            long +
            "&key=AIzaSyDbDLtySKbZePECwNvxTaqzck57bN9NzA8"
        )
        .then((res) => {
          let citySplit = res.data.plus_code.compound_code.split(" ");
          this.city = citySplit.slice(1, 4).join(" ");
        });
    },
    geolocationCheck() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            this.lattitude = position.coords.latitude;
            this.longitude = position.coords.longitude;
            this.getUsersLocation(this.lattitude, this.longitude);
            this.getCity(this.lattitude, this.longitude);
          },
          (error) => {
            console.log(error.message);
          }
        );
      } else {
        console.log("Your browser does not support geolocation");
      }
    },
  },
  mounted() {
    this.geolocationCheck();
    setInterval(() => {
      this.geolocationCheck();
    }, 300000);
  },
  // TODO: Possibly add a watch function and create the if statements in there, allowing for the WeatherBackground component to be called only once already containing the container class and the specific background classes being added based off their corresponding weatherId numbers
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@400;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Alfa+Slab+One&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

img {
  height: auto;
  width: 100%;
}

#app {
  font-family: "Raleway", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 18px;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container.clear {
  background: url("./assets/clear.jpg") center no-repeat;
  background-size: cover;
}
.container.atmosphere {
  background: url("./assets/atmosphere.jpg") center no-repeat;
  background-size: cover;
}
.container.clouds {
  background: url("./assets/clouds.jpg") center no-repeat;
  background-size: cover;
}
.container.drizzle {
  background: url("./assets/drizzle.jpg") center no-repeat;
  background-size: cover;
}
.container.rain {
  background: url("./assets/rain.jpg") center no-repeat;
  background-size: cover;
}
.container.snow {
  background: url("./assets/snow.jpg") center no-repeat;
  background-size: cover;
}
.container.thunderstorm {
  background: url("./assets/thunderstorm.jpg") center no-repeat;
  background-size: cover;
}
</style>
