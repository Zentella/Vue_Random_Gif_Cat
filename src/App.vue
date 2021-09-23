<template>
  <div id="app">
    <random />
  </div>
</template>

<script>
import random from "./components/random.vue";

export default {
  name: "App",
  components: {
      random,
  },
  data() {
    return {
    };
  },
};
</script>