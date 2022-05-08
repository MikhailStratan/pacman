<template>
    <div 
        class="map-block"
        :style="{backgroundImage: blockImage, width: scale.value + 'px', height: scale.value + 'px'}">
        <map-score v-if="blockType === 1"></map-score>
        
    </div>
</template>

<script>
import MapScore from './MapScore.vue';

export default {
    components: {
        MapScore
    },
    inject: ['scale'],
    props: {
        blockType: Number
    },
    data() {
        return {
            isBorder: this.border,
        }
    },
    computed: {
        blockImage() {
            if (this.blockType === 0) return `url(${require('@/assets/img/box-1.jpg')})`;
            
            else if (this.blockType === 3) return `url(${require('@/assets/img/pacman-img.png')})`;
            else if (this.blockType === 20) return `url(${require('@/assets/img/ghost-blue.png')})`;
            else if (this.blockType === 21) return `url(${require('@/assets/img/ghost-green.png')})`;
            else if (this.blockType === 22) return `url(${require('@/assets/img/ghost-red.png')})`;
            else if (this.blockType === 23) return `url(${require('@/assets/img/ghost-yellow.png')})`;
            else return '';
        },
        blockColor() {
            if (this.blockType === 1) return `black`;
            else return '';
        }
    }
}
</script>

<style>
    .map-block {
        display: inline-block;

        background-size: cover;
        padding: 0;
        margin: 0;
    }

</style>