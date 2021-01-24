<template>
  <div id="city">
    <p>{{ city }}</p>
  </div>
</template>

<script>
export default {
  props: ["city"],
};
</script>

<style scoped>
p {
  margin-bottom: 20px;
}
</style>