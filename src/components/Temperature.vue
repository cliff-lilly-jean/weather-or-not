<template>
  <div id="temperature">
    <p class="degree">{{ temp }}&deg;</p>
    <div class="weather-details">
      <p class="detail">
        <img src="../assets/icons/windSpeed.svg" alt="" />
        {{ windSpeed }}
      </p>
      <p class="detail">
        <img src="../assets/icons/humidity.svg" alt="" /> {{ humidity }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["temp", "humidity", "windSpeed"],
};
</script>

<style scoped>
.degree {
  font-size: 5rem;
  text-align: center;
  margin: 10px auto;
  font-weight: bold;
  font-family: "Alfa Slab One", cursive;
}

.weather-details {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.detail {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.detail img {
  max-width: 20px;
  width: 100%;
  margin-right: 5px;
}
</style>