<template>
    <map-scale @scaleChange="setScale"></map-scale>
    <div 
        class="map"
        :style="{width: scale*blocksPerLine + 'px'}">
        <map-generator></map-generator>
    </div>
</template>

<script>
import { computed } from "vue";
import MapGenerator from "./MapGenerator.vue";
import MapScale from "./MapScale.vue";


export default {
    components: {
        MapGenerator,
        MapScale
    },
    inject: ['map'],
    provide() {
        return {
            scale: computed(() => this.scale),
        }
    },
    data() {
        return {
            scale: this.map.length,
            blocksPerLine: this.map[0].length
        }
    },
    methods: {
        setScale(scaleValue) {
            this.scale = scaleValue;
        },
    }

}
</script>

<style>
    .map {
        display: block;
        margin: 0 auto;
    }
</style>