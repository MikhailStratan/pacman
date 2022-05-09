<template>
    <h2 class="title">Pacman</h2>
    <map-container></map-container>
    <actor-pacman></actor-pacman>
</template>

<script>
import MapContainer from './components/map/MapContainer.vue'
import ActorPacman from './components/actors/ActorPacman.vue';
import mapsSchemes from './assets/maps/index';

export default {
    name: 'App',
    components: {
        MapContainer,
        ActorPacman
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
