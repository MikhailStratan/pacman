<template>
  <h2 class="title">Pacman</h2>
  <map-container></map-container>
</template>

<script>
import MapContainer from './components/map/MapContainer.vue'

export default {
  name: 'App',
  components: {
    MapContainer
  }
}
</script>

<style>
  #app {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: black;
  }

  .title {
    color: white;
    margin: 15px auto;
    text-align: center;
  }

  
</style>
