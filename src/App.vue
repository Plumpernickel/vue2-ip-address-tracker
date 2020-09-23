<template>
  <div id="app">
    <MapOverlay />
  </div>
</template>

<script>
import MapOverlay from './components/MapOverlay.vue';

export default {
  name: 'App',
  components: {
    MapOverlay,
  },
};
</script>

<style lang="scss">
html, body {
  margin: 0;
  padding: 0;

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    background-image: url('./assets/pattern-bg.png');
    background-size: contain;
  }
}
</style>
