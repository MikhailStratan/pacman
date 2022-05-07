<template>
    <map-scale @scaleChange="setScale"></map-scale>
    <div 
        class="map"
        :style="{width: scale*25 + 'px'}" >
       
        <map-generator></map-generator>
    </div>
</template>

<script>
import { computed } from "vue";
import MapGenerator from "./MapGenerator.vue";
import MapScale from "./MapScale.vue";
import mapsSchemes from '../../assets/maps/index.js';

export default {
    components: {
        MapGenerator,
        MapScale
    },
    provide() {
        return {
            scale: computed(() => this.scale),
            maps: this.maps
        }
    },
    data() {
        return {
            scale: 25,
            maps: mapsSchemes,
        }
    },
    methods: {
        setScale(scaleValue) {
            this.scale = scaleValue;
        }
    }

}
</script>

<style>
    .map {
        display: block;
        margin: 0 auto;
    }
</style>