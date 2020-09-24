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
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap');

html, body {
  margin: 0;
  padding: 0;
  font-family: 'Rubik', Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  #app {
    padding: 20px 0;
    text-align: center;
    background-image: url('./assets/pattern-bg.png');
    background-size: contain;
    background-repeat: no-repeat;

    @media screen and (max-width: 667px) {
      background-size: auto;
    }
  }
}
</style>
