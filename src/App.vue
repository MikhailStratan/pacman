<template>
    <h2 class="title">Pacman</h2>
    <map-container></map-container>
    <move-pacman></move-pacman>
</template>

<script>
import MapContainer from './components/map/MapContainer.vue'
import MovePacman from './components/controllers/MovePacman.vue';
import mapsSchemes from './assets/maps/index';

export default {
    name: 'App',
    components: {
        MapContainer,
        MovePacman
    },
    provide() {
        return {
            map: this.maps.level1
        }
    },
    data() {
        return {
            maps: { ...mapsSchemes }
        }
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
