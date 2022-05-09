<template>
    <div 
        class="map-line"
        v-for="(line, indexY) in map" 
        :key="indexY">
            <map-block
                v-for="(block, indexX) in map[0]"
                :key="''+indexX+indexY"
                :blockType="map[indexY][indexX]"></map-block>
    </div>
</template>

<script>

import MapBlock from './MapBlock.vue';

export default {
    components: {
        MapBlock
    },
    inject: ['scale', 'map'],
    data() {
        return {

            mapSize: {
                vertivalSize: this.map.length,
                horizontalSize: this.map[0].length,
            }
        }
    },
    created() {
        console.log(this.map)
    }
}
</script>

<style>
    *{
        box-sizing: border-box;
    }
   
    .map-line {
        display: grid;
        grid-template-columns: repeat(25, 1fr);
        grid-template-rows: 1fr;
        gap: 0px;
    }
</style>