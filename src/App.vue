<template>
  <div id="app">
    <test-app></test-app>
  </div>
</template>

<script>
import Test from "./components/Test.vue";

export default {
  name: "App",
  components: {
    "test-app": Test,
  },
};
</script>

<style></style>
