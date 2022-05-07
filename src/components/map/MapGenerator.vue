<template>
    <div 
        class="map-line"
        
        v-for="(line, indexY) in maps.level1" 
        :key="indexY">
            <map-block
                v-for="(block, indexX) in maps.level1[0]"
                :key="indexX"
                :blockType="maps.level1[indexY][indexX]"></map-block>
    </div>
</template>

<script>

import MapBlock from './MapBlock.vue';

export default {
    components: {
        MapBlock
    },
    inject: ['scale', 'maps'],
    data() {
        return {

            mapSize: {
                vertivalSize: this.maps.level1.length,
                horizontalSize: this.maps.level1[0].length,
            }
        }
    },
    created() {
        console.log(this.maps.level1)
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