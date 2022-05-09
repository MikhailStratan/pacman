<template>
    <move-pacman>
        
    </move-pacman>
</template>

<script>
import MovePacman from "../controllers/MovePacman.vue";
export default {
    components: { 
        MovePacman 
    },
    props: {
        color: String,
        blockType: String
    },
    inject: ['map'],
    
    provide() {
        return {
            position: this.position,
            speed: this.speed,
            updatePosition: this.updateGhostPosition,
            actor: "ghost",
            blockType: this.blockType,
            leftover: this.leftover
        };
    },
    data() {
        return {
            position: {
                y: null,
                x: null,
            },
            speed: 300,
            leftover: 1
        };
    },
    methods: {
        setGhostPosition() {
            this.map.forEach((mapLine, indexY) => {
                mapLine.forEach((item, indexX) => {
                    if (item === this.blockType) {
                        this.updateGhostPosition(indexY, indexX);
                    }
                });
            });
        },
        updateGhostPosition(y, x) {
            this.position.previous = {
                y: this.position.y,
                x: this.position.x
            };
            this.position.y = y;
            this.position.x = x;
            console.log(this.position);
        },
    },
    created() {
        this.setGhostPosition();
        console.log(this.positions);
    },
    
}
</script>