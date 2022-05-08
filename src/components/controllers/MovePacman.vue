<template>
    <div>
        
    </div>
</template>

<script>
export default {
    inject: ['map'],
    emits: ['moveUp'],
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
            movesListener: null,

        }
    },
    methods: {
        move(direction) {
                let newX, newY;
                switch (direction) {
                    case 'up':
                        newX = this.position.x;
                        newY = this.position.y - 1;
                        break;
                    case 'down':
                        newX = this.position.x;
                        newY = this.position.y + 1;
                        break;
                    case 'left':
                        newX = this.position.x - 1;
                        newY = this.position.y;
                        break;
                    case 'right':
                        newX = this.position.x + 1;
                        newY = this.position.y;
                        break;
                    default:
                        break;
                }

                this.map[newY][newX] = 3;
                this.updatePacmanPosition(newY, newX);
                this.setLeftover(this.position.previous.y,this.position.previous.x);

            console.log(this.position)
        },

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
        },

        setLeftover(y,x) {
            this.map[y][x] = 2;
        },

        addMovesListener() {
            this.movesListener = addEventListener('keydown', (event) => {
                event.preventDefault();
                if (event.code === 'ArrowUp') this.move('up');
                if (event.code === 'ArrowDown') this.move('down');
                if (event.code === 'ArrowRight') this.move('right');
                if (event.code === 'ArrowLeft') this.move('left');
                
            });
        }

    },
    created() {
        this.definePacmanPosition();
        this.addMovesListener();
        console.log(this.position)
    }
}
</script>