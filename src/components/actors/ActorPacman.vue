<template>
    <move-pacman>
        
    </move-pacman>
</template>

<script>
import MovePacman from "../controllers/MovePacman.vue";

export default {
    inject: ['map'],
    components: {
        MovePacman
    },
    provide() {
        return {
            position: this.position,
            speed: this.speed,
            leftover: this.leftover,
            updatePacmanPosition: this.updatePacmanPosition,
        }
    },
    data() {
        return {
            position: {
                y: null,
                x: null,
                previous: {
                    x: null,
                    y: null,
                }
            },
            speed: 300,
            leftover: 2
        }
    },
    watch: {
        position() {
            console.log(this.position)
        }
    },
    methods: {
        definePacmanPosition() {
            this.map.forEach((mapLine, indexY) => {
                mapLine.forEach((item, indexX) => {
                    if (item === 3) {
                        this.updatePacmanPosition(indexY,indexX)
                    }
                })
            });
        },

        updatePacmanPosition(y,x) {
            this.position.previous = {
                y: this.position.y,
                x: this.position.x
            }
            this.position.y = y;
            this.position.x = x;
            console.log(this.position);
        },


    },
    created() {
        this.definePacmanPosition();
    }
}
</script>