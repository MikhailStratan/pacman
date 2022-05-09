<template>
    <div>

    </div>
</template>

<script>
export default {
    inject: [
        'map',
        'position',
        'speed',
        'updatePosition',
        'leftover',
        'actor',
        'blockType'
    ],
    emits: ['moveUp'],
    data() {
        return {
            movesListener: null,
            movesInterval: null,
            possibleWays: {
                up: null,
                down: null,
                left: null,
                right: null
            },
            way: null
        }
    },
    watch: {
        possibleWays() {
            for (let way in this.possibleWays) {
                if (this.possibleWays[way] === false && way === this.way) {
                    console.log(`Can't go ${way}`)
                    clearInterval(this.movesInterval);
                }
            }
        }
    },
    methods: {
        move(direction) {
            this.updatePossibleWays();
            let newX, newY;

            if (direction === 'up' && this.possibleWays.up) {
                newX = this.position.x;
                newY = this.position.y - 1;
            } else if (direction === 'down' && this.possibleWays.down) {
                newX = this.position.x;
                newY = this.position.y + 1;
            } else if (direction === 'left' && this.possibleWays.left) {
                newX = this.position.x - 1;
                newY = this.position.y;
            } else if (direction === 'right' && this.possibleWays.right) {
                newX = this.position.x + 1;
                newY = this.position.y;
            }

            this.way = direction;
            this.map[newY][newX] = this.blockType;
            this.updatePosition(newY, newX);
            if (this.leftover) {
                this.setLeftover(this.position.previous.y, this.position.previous.x);
            }
            console.log('works')
        },

        randomMove() {
            this.updatePossibleWays();
            const possibleWaysArray = Object.keys(this.possibleWays).filter(way => this.possibleWays[way]);
            const randomChoose = Math.floor(Math.random() * possibleWaysArray.length);
            
            if (possibleWaysArray.includes(this.way)) {
                this.move(this.way);
                return;
            }
            this.move(possibleWaysArray[randomChoose]);
        },

        setLeftover(y, x) {
            this.map[y][x] = this.leftover;
        },

        addPacmanMovesListener() {
            console.log('added')
            this.movesListener = addEventListener('keydown', (event) => {
                event.preventDefault();
                if (event.code === 'ArrowUp') this.startMoves(() => this.move('up'));
                if (event.code === 'ArrowDown') this.startMoves(() => this.move('down'));
                if (event.code === 'ArrowRight') this.startMoves(() => this.move('right'));
                if (event.code === 'ArrowLeft') this.startMoves(() => this.move('left'));
                
            });
        },

        addGhostMoves(moveCallback) {
            this.movesInterval = setInterval(moveCallback, this.speed);
        },

        startMoves(moveCallback) {
            if (this.movesInterval) {
                clearInterval(this.movesInterval)
            }
            console.log(moveCallback, this.speed)
            this.movesInterval = setInterval(moveCallback, this.speed)
        },

        updatePossibleWays() {
            const y = this.position.y;
            const x = this.position.x;
            this.possibleWays = {
                up: this.map[y - 1][x] === 0 ? false : true,
                down: this.map[y + 1][x] === 0 ? false : true,
                left: this.map[y][x - 1] === 0 ? false : true,
                right: this.map[y][x + 1] === 0 ? false : true,
            }
        },

    },
    created() {
        this.updatePossibleWays();
        console.log(this.possibleWays)
        if (this.actor === 'pacman') {
            this.addPacmanMovesListener();
        } else {
            this.addGhostMoves(() => this.randomMove());
        }
        
    }
}
</script>