<script setup>
import gameIcons from '../utils/gameIcons.js';
const gameMap = new Map([
        ['scissors', ['paper', 'lizard']],
        ['paper', ['rock', 'spock']],
        ['rock', ['lizard', 'scissors']],
        ['lizard', ['spock', 'paper']],
        ['spock', ['scissors', 'rock']]
]);


// - Scissors beats Paper
// - Scissors beats Lizard
// - Paper beats Rock
// - Paper beats Spock
// - Rock beats Lizard
// - Rock beats Scissors
// - Lizard beats Spock
// - Lizard beats Paper
// - Spock beats Scissors
// - Spock beats Rock

</script>

<template>
        <div class="buttons">
<!-- 
                <svg class="line1">
                        <line x1="68.32" y1="68.32" x2="168.32" y2="34.16" stroke-width="15" />
                </svg>
                <svg class="line2">
                        <line x1="68.32" y1="68.32" x2="168.32" y2="34.16" stroke-width="15" />
                </svg>
                <svg class="line3">
                        <line x1="68.32" y1="68.32" x2="168.32" y2="34.16" stroke-width="15" />
                </svg>
                <svg class="line4">
                        <line x1="68.32" y1="68.32" x2="168.32" y2="34.16" stroke-width="15" />
                </svg>
                <svg class="line5">
                        <line x1="68.32" y1="68.32" x2="168.32" y2="34.16" stroke-width="15" />
                </svg> -->

                <button class="btn btn-scissors">

                        <img :src="gameIcons[0]" alt="Scissors" />
                </button>
                <button class="btn btn-spock">
                        <img :src="gameIcons[1]" alt="Spock" />
                </button>
                <button class="btn btn-paper">
                        <img :src="gameIcons[2]" alt="Paper" />
                </button>
                <button class="btn btn-lizard">
                        <img :src="gameIcons[3]" alt="Lizard" />
                </button>
                <button class="btn btn-rock">
                        <img :src="gameIcons[4]" alt="Rock" />
                </button>
        </div>
</template>

<style scoped>
        .buttons {
                display: flex;
                justify-content: space-between;
                gap: 1rem;
                position: relative;
                min-width: 22svw;
                max-width: 25svw;
                width: auto;
                margin: 0 auto;
                aspect-ratio: 1 / 1;
                background-image: url('../assets/images/bg-pentagon.svg');
                background-repeat: no-repeat;
                background-size: 90%;
                background-position: center;
        }
        .btn {
                --btn-distance: 2svw;
                position: absolute;
                min-width: 2svw;
                max-width: 30%;
                width: 100%;
                display: grid;
                place-items: center;
                aspect-ratio: 1 / 1;
                border-radius: 50%;
                border: none;
                z-index: 9;
                border: double 10px transparent;
                border-radius: 50%;
                background-origin: border-box;
                background-clip: content-box, border-box;
                padding-inline: 0;
        }
        .btn > img {
                max-width: 50%;
        }
        
        .btn:nth-of-type(1) {
                top: 0;
                left: 50%;
                transform: translateX(-50%) scale(1);
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--scissors-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--scissors-color-opacity);
        }
                
        .btn:nth-of-type(2) {
                top: 28%;
                left: 0%;
                background-image: linear-gradient(white, white), radial-gradient(var(--spock-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--spock-color-opacity);
                }
                
        .btn:nth-of-type(3) {
                top: 28%;
                right: 0%;
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--paper-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--paper-color-opacity);
        }
        
        .btn:nth-of-type(4) {
                bottom: 0;
                left: 10%;
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--lizard-gradient));
                box-shadow:
                                inset 0 6px rgba(0, 0, 0, 0.2),
                                0 6px var(--lizard-color-opacity);
        }
        
        .btn:nth-of-type(5) {
                bottom: 0;
                right: 10%;
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--rock-gradient));
                box-shadow:
                                inset 0 6px rgba(0, 0, 0, 0.2),
                                0 6px var(--rock-color-opacity);
        }
        .btn:hover {
                transform: scale(1.07);
                cursor: pointer;
        }
        .btn:hover > img {
                transform: scale(1.1) rotate(10deg);
                cursor: pointer;
        }
        .btn:nth-of-type(1):hover {
                transform: translateX(-50%) scale(1.07);
        }

        .line1, .line2, .line3, .line4, .line5 {
                position: absolute;
                stroke: rgba(0, 0, 0, 0.4);
        }
        .line1 {
                top: 50%;
                left: 50%;
                transform: translate(-62%, -87%) rotate(-19deg);
                z-index: 1;
        }
        .line2 {
                top: 50%;
                left: 50%;
                transform: translate(-24%, -69%) rotate(57deg);
                z-index: 1;
        }
        .line3 {
                top: 50%;
                left: 50%;
                transform: translate(-27%, 5%) rotate(128deg);
                z-index: 1;
        }
        .line4 {
                top: 50%;
                left: 50%;
                transform: translate(-40%, 60%) rotate(18deg);
                z-index: 1;
        }
        .line5 {
                top: 50%;
                left: 50%;
                transform: translate(-90%, 10%) rotate(88deg);
                z-index: 1;
        }
        @media (max-width: 768px) {
                .buttons {
                        max-width: 90%;
                        width: auto;
                }
        }
        @media (max-width: 1024px) {
                .buttons {
                        max-width: 50%;
                        width: auto;
                }
        }
</style>
