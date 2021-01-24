<template>
  <div id="icon">
    <img class="iconImage" :src="getImage(icon)" alt="" />
  </div>
</template>

<script>
export default {
  props: ["icon"],

  methods: {
    getImage(image) {
      return require("../assets/icons/" + image + ".svg");
    },
  },
};
</script>

<style scoped>
#icon {
  margin: 0 auto;
}

.iconImage {
  width: 300px;
  height: 300px;
  filter: drop-shadow(10px 15px 10px rgba(0, 0, 0, 0.4));
  margin-top: -3em;
  margin-bottom: -4em;
}
</style>