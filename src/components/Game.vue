<script setup>
import { ref, inject, watchEffect, onMounted } from 'vue';
import gameIcons from '../utils/gameIcons.js';

const gameMap = new Map([
        ['scissors', ['paper', 'lizard']],
        ['paper', ['rock', 'spock']],
        ['rock', ['lizard', 'scissors']],
        ['lizard', ['spock', 'paper']],
        ['spock', ['scissors', 'rock']]
]);


let isComputerLoading = ref(false);
let resultString = ref('');
let playerChoice = ref('');
let computerChoice = ref('');
let score = inject('score');
let resultsBeShown = ref(false);
let isPlayAgain = ref(false);


const handlePlayerChoice =  (choice) => {
        playerChoice.value = choice;
        resultsBeShown.value = true;
        console.log(playerChoice.value);
        isComputerLoading.value = true;
        generateComputerChoice();
        determineWinner();

};

const generateComputerChoice =  () => {
        const choices = Array.from(gameMap.keys());
        const randomIndex = Math.floor(Math.random() * choices.length);
        computerChoice.value = choices[randomIndex];
};

const determineWinner =  () => {
        setTimeout(() => {
                if (playerChoice.value === computerChoice.value) {
                        resultString.value = 'It\'s a tie';
                } else if (gameMap.get(playerChoice.value).includes(computerChoice.value)) {
                        resultString.value = 'you win';
                        score.value++;
                } else {
                        resultString.value = 'you lose';
                        score.value == 0 ? score.value : score.value--;
                }
                isComputerLoading.value = false;
                isPlayAgain.value = true;
                localStorage.setItem('score', score.value);
        }, 2000);
};

const playAgain =  () => {
        resultsBeShown.value = false;
        playerChoice.value = '';
        computerChoice.value = '';
        resultString.value = '';
        isPlayAgain.value = false;
};

onMounted(() => {
        if (localStorage.getItem('score')) {
                score.value = parseInt(localStorage.getItem('score'));
        }
});

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
        <div class="buttons" v-if="!resultsBeShown">

                <button class="btn btn-scissors picking" aria-label="scissors" @click="handlePlayerChoice('scissors')">
                        <img :src="gameIcons[0]" alt="Scissors" />
                </button>
                <button class="btn btn-spock" aria-label="spock" @click="handlePlayerChoice('spock')">
                        <img :src="gameIcons[1]" alt="Spock" />
                </button>
                <button class="btn btn-paper" aria-label="paper" @click="handlePlayerChoice('paper')">
                        <img :src="gameIcons[2]" alt="Paper" />
                </button>
                <button class="btn btn-lizard" aria-label="lizard" @click="handlePlayerChoice('lizard')">
                        <img :src="gameIcons[3]" alt="Lizard" />
                </button>
                <button class="btn btn-rock" aria-label="rock" @click="handlePlayerChoice('rock')">
                        <img :src="gameIcons[4]" alt="Rock" />
                </button>
        </div>

        <div class="results" v-if="resultsBeShown">
                <div class="yourPick" v-if="playerChoice">
                        <p>You Picked</p>
                        <button v-if="playerChoice === 'scissors'"
                                :class="'btn ' + (playerChoice === 'scissors' ? 'btn-scissors picked' : '')"
                                aria-label="scissors">
                                <img :src="gameIcons[0]" alt="Scissors" />
                        </button>
                        <button v-if="playerChoice === 'spock'"
                                :class="'btn ' + (playerChoice === 'spock' ? 'btn-spock picked' : '')"
                                aria-label="spock">
                                <img :src="gameIcons[1]" alt="Spock" />
                        </button>
                        <button v-if="playerChoice === 'paper'"
                                :class="'btn ' + (playerChoice === 'paper' ? 'btn-paper picked' : '')"
                                aria-label="paper">
                                <img :src="gameIcons[2]" alt="Paper" />
                        </button>
                        <button v-if="playerChoice === 'lizard'"
                                :class="'btn ' + (playerChoice === 'lizard' ? 'btn-lizard picked' : '')"
                                aria-label="lizard">
                                <img :src="gameIcons[3]" alt="Lizard" />
                        </button>
                        <button v-if="playerChoice === 'rock'"
                                :class="'btn ' + (playerChoice === 'rock' ? 'btn-rock picked' : '')" aria-label="rock">
                                <img :src="gameIcons[4]" alt="Rock" />
                        </button>
                </div>

                <div class="resultString" v-if="resultString">
                        <h3>
                                {{ resultString }}
                        </h3>
                </div>
                <div class="loading" v-if="isComputerLoading">
                        <div class="ball"></div>
                        <div class="ball"></div>
                        <div class="ball"></div>
                        <div class="ball"></div>
                        <div class="ball"></div>
                        <div class="ball"></div>
                        <div class="ball"></div>
                </div>

                <div class="computerPick" v-if="computerChoice && !isComputerLoading">
                        <p>The house Picked</p>


                        <button v-if="computerChoice === 'scissors'"
                                :class="'btn ' + (computerChoice === 'scissors' ? 'btn-scissors picked' : '')"
                                aria-label="scissors">
                                <img :src="gameIcons[0]" alt="Scissors" />
                        </button>
                        <button v-if="computerChoice === 'spock'"
                                :class="'btn ' + (computerChoice === 'spock' ? 'btn-spock picked' : '')"
                                aria-label="spock">
                                <img :src="gameIcons[1]" alt="Spock" />
                        </button>
                        <button v-if="computerChoice === 'paper'"
                                :class="'btn ' + (computerChoice === 'paper' ? 'btn-paper picked' : '')"
                                aria-label="paper">
                                <img :src="gameIcons[2]" alt="Paper" />
                        </button>
                        <button v-if="computerChoice === 'lizard'"
                                :class="'btn ' + (computerChoice === 'lizard' ? 'btn-lizard picked' : '')"
                                aria-label="lizard">
                                <img :src="gameIcons[3]" alt="Lizard" />
                        </button>
                        <button v-if="computerChoice === 'rock'"
                                :class="'btn ' + (computerChoice === 'rock' ? 'btn-rock picked' : '')"
                                aria-label="rock">
                                <img :src="gameIcons[4]" alt="Rock" />
                        </button>
                </div>

        </div>

        <div class="resetButtons" v-if="resultsBeShown && computerChoice && playerChoice && isPlayAgain">
                <button @click="playAgain()">play again</button>
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
        
        .btn.btn-scissors {
                top: 0;
                left: 50%;
                transform: translateX(-50%) scale(1);
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--scissors-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--scissors-color-opacity);
        }
                
        .btn.btn-spock {
                top: 28%;
                left: 0%;
                background-image: linear-gradient(white, white), radial-gradient(var(--spock-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--spock-color-opacity);
                }
                
        .btn.btn-paper {
                top: 28%;
                right: 0%;
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--paper-gradient));
                box-shadow: 
                        inset 0 6px rgba(0, 0, 0, 0.2),
                        0 6px var(--paper-color-opacity);
        }
        
        .btn.btn-lizard {
                bottom: 0;
                left: 10%;
                background-image: linear-gradient(white, white), radial-gradient(circle at top left, var(--lizard-gradient));
                box-shadow:
                                inset 0 6px rgba(0, 0, 0, 0.2),
                                0 6px var(--lizard-color-opacity);
        }
        
        .btn.btn-rock {
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
        .btn.btn-scissors:hover {
                transform: translateX(-50%) scale(1.07);
        }
        .btn.picked:hover, .btn.btn-scissors.picked {
                transform: translateX(0%) scale(1) !important;
        }

        .results {
                display: grid;
                grid-template-columns: 1fr .5fr 1fr;
                gap: 1rem;
                align-items: center;
                justify-content: center;
                position: relative;
                max-width: 70%;
                width: auto;
                height: auto;
                margin: 0 auto;
        }

        .yourPick {
                grid-column: 1;
                display: grid;
                place-items: center;
                width: 100%;
                height: 100%;
        }
        .resultString {
                grid-column: 2;
                display: grid;
                place-items: center;
                width: 100%;
                height: 100%;
        }
        .computerPick {
                grid-column: 3;
                display: grid;
                place-items: center;
                width: 100%;
                height: 100%;
        }
        .yourPick p, .computerPick p {
                font-size: clamp(1rem, 2vw, 1.5rem);
                font-weight: 700;
                letter-spacing: 3px;
                text-transform: uppercase;
                color: white;
        }

        .results .yourPick:has(button.picked) button {
                position: relative;
                z-index: 1;
                left: 0;
                top: 10%;
        }
        .results .computerPick:has(button.picked) button {
                position: relative;
                z-index: 1;
                left: 0;
                top: 10%;
        }
        .results .resultString:has(h3) h3 {
                font-size: clamp(3rem, 3vw, 2rem);
                font-weight: 700;
                letter-spacing: 3px;
                text-transform: uppercase;
                color: white;
        }

        .resetButtons {
                display: grid;
                place-items: center;
        }
        .resetButtons button {
                padding: 1em 3em;
                font-size: clamp(1rem, 1.5vw, 1.2rem);
                font-family: inherit;
                font-weight: 700;
                letter-spacing: 3px;
                text-transform: uppercase;
                background-color: #ffffff;
                color: hsl(214, 47%, 23%);
                border: none;
                border-radius: 10px;
                cursor: pointer;
        }
        .resetButtons button:hover {
                background-color: hsl(214, 47%, 23%);
                color: #ffffff;
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


        .loading {
                width: 200px;
                height: 100px;
                margin: 0 auto;
        }

        .ball {
                width: 10px;
                height: 10px;
                margin: 10px auto;
                border-radius: 50px;
        }

        .ball:nth-child(1) {
                background: #ffffff;
                -webkit-animation: right 1s infinite ease-in-out;
                -moz-animation: right 1s infinite ease-in-out;
                animation: right 1s infinite ease-in-out;
        }

        .ball:nth-child(2) {
                background: #ffffff;
                -webkit-animation: left 1.1s infinite ease-in-out;
                -moz-animation: left 1.1s infinite ease-in-out;
                animation: left 1.1s infinite ease-in-out;
        }

        .ball:nth-child(3) {
                background: #ffffff;
                -webkit-animation: right 1.05s infinite ease-in-out;
                -moz-animation: right 1.05s infinite ease-in-out;
                animation: right 1.05s infinite ease-in-out;
        }

        .ball:nth-child(4) {
                background: #ffffff;
                -webkit-animation: left 1.15s infinite ease-in-out;
                -moz-animation: left 1.15s infinite ease-in-out;
                animation: left 1.15s infinite ease-in-out;
        }

        .ball:nth-child(5) {
                background: #ffffff;
                -webkit-animation: right 1.1s infinite ease-in-out;
                -moz-animation: right 1.1s infinite ease-in-out;
                animation: right 1.1s infinite ease-in-out;
        }

        .ball:nth-child(6) {
                background: #ffffff;
                -webkit-animation: left 1.05s infinite ease-in-out;
                -moz-animation: left 1.05s infinite ease-in-out;
                animation: left 1.05s infinite ease-in-out;
        }

        .ball:nth-child(7) {
                background: #ffffff;
                -webkit-animation: right 1s infinite ease-in-out;
                -moz-animation: right 1s infinite ease-in-out;
                animation: right 1s infinite ease-in-out;
        }

        @-webkit-keyframes right {
                0% {
                        -webkit-transform: translate(-15px);
                }

                50% {
                        -webkit-transform: translate(15px);
                }

                100% {
                        -webkit-transform: translate(-15px);
                }
        }

        @-webkit-keyframes left {
                0% {
                        -webkit-transform: translate(15px);
                }

                50% {
                        -webkit-transform: translate(-15px);
                }

                100% {
                        -webkit-transform: translate(15px);
                }
        }

        @-moz-keyframes right {
                0% {
                        -moz-transform: translate(-15px);
                }

                50% {
                        -moz-transform: translate(15px);
                }

                100% {
                        -moz-transform: translate(-15px);
                }
        }

        @-moz-keyframes left {
                0% {
                        -moz-transform: translate(15px);
                }

                50% {
                        -moz-transform: translate(-15px);
                }

                100% {
                        -moz-transform: translate(15px);
                }
        }

        @keyframes right {
                0% {
                        transform: translate(-15px);
                }

                50% {
                        transform: translate(15px);
                }

                100% {
                        transform: translate(-15px);
                }
        }

        @keyframes left {
                0% {
                        transform: translate(15px);
                }

                50% {
                        transform: translate(-15px);
                }

                100% {
                        transform: translate(15px);
                }
        }


        @media (max-width: 768px) {
                .buttons {
                        max-width: 90%;
                        width: auto;
                }
                .results {
                        grid-template-columns: 1fr 1fr;
                        grid-template-rows: 1fr 1fr;
                        max-width: 90%;
                        gap: 1rem;
                }

                .yourPick,
                .computerPick{
                        width: 50%;
                        display: flex;
                        flex-direction: column-reverse;
                        gap: 2rem;
                }
                .yourPick {
                        grid-row: 1;
                        width: 100%;
                }
                .computerPick {
                        grid-column: 2;
                        grid-row: 1;
                        width: 100%;
                }
                .resultString {
                        grid-column: 1 / span 2;
                        font-size: clamp(3rem, 4vw, 3rem);
                }
                .yourPick p, .computerPick p {
                        font-size: clamp(.9rem, 1vw, 1.5rem);
                        font-weight: 700;
                        letter-spacing: 2px;
                        text-transform: uppercase;
                        color: white;
                }
                .yourPick button, .computerPick button {
                        max-width: 60% !important;
                }

        }
        @media (max-width: 1024px) {
                .buttons {
                        max-width: 50%;
                        width: auto;
                }
        }
</style>