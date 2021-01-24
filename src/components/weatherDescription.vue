<template>
  <div class="weather-description">
    <p class="description">{{ weatherDescription }}</p>
  </div>
</template>

<script>
export default {
  props: ["weatherDescription"],
};
</script>

<style scoped>
.description {
  text-align: center;
  color: #2f2f2f;
  font-family: "Alfa Slab One", cursive;
}
</style>