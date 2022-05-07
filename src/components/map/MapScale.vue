<template>
    <div class="map-scale">
        <label for="scale">Scale:</label>
        <input type="range" name="scale" min="10" max="50" v-model="scale"/>
    </div>
</template>

<script>
export default {
    emits: ['scaleChange'],
    data() {
        return {
            scale: 25
        }
    },
    watch: {
        scale(value) {
            //console.log(value)
            this.$emit('scaleChange', value);
        }
    },
}
</script>

<style scoped>
    .map-scale {
        display: block;
        position: absolute;
        left: 25px;
        width: 100%;
        margin: 25px auto;
        color: white;
    }

    label {
        position: relative;
        padding-right: 5px;
        top: -3px;
    }
</style>