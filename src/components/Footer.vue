<script setup>
        import { provide, ref } from 'vue';
        let showRules = ref(false);
        provide('showRules', showRules);
</script>

<template>
        <footer>
                <p>Challenge by <a href="www.frontendmentor.io" target="_blank">FrontEnd Mentor</a> / developed by <a
                                href="https://github.com/FabbSantos" target="_blank">Fabrício Bahiense</a></p>
                <p>Find me <a href="https://fabs-work.vercel.app/" target="_blank">here</a></p>

                <button @click="showRules = true">
                        Rules
                </button>

                <div class="modal" v-if="showRules">
                        <img src="../assets/images/image-rules-bonus.svg" alt="Rules of the game        ">

                        <button @click="showRules = !showRules"> <img src="../assets/images/icon-close.svg"
                                        alt="Close Rules"></button>
                </div>
        </footer>
</template>

<style scoped>

        footer {
                width: 90%;
                display: flex;
                justify-content: space-between;
                align-items: end;
                padding-inline: 2rem;
                font-size: clamp(.2rem, .3vw, .6rem);
                font-weight: 700 !important;
                text-transform: uppercase;
                letter-spacing: 2px;
                color: var(--header-outline);
                position: absolute;
                bottom: 2%;
                left: 0;
        }
        a {
                color: var(--header-outline);
                text-decoration: wavy underline 1px; 
                text-underline-offset: 3px; 
        }
        .modal {
                width: 100svw;
                height: 100svh;
                background-color: rgba(0, 0, 0, .9);
                position: fixed;
                top: 0;
                left: 0;
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 100;
        }
        button, button > img {
                cursor: pointer;
        }
        button {
                background-color: transparent;
                color: white;
                padding: .6rem 2rem;
                border: 1px solid var(--header-outline);
                border-radius: 5px;
                text-transform: uppercase;
                font-family: inherit;
                letter-spacing: 2px;
        }
        button:hover {
                background-color: var(--header-outline);
                color: white;
        }
        .modal button {
                background-color: rgba(255, 255, 255, 1);
                border: none;
                position: absolute;
                top: 40%;
                right:30%;
                display: grid;
                place-items: center;
                padding: .5rem;
                border-radius: 50%;
        }

        @media (max-width: 768px){
                footer{
                        font-size: clamp(.1rem, .1vw, .2rem);
                        width: 100%;
                        flex-direction: column-reverse;
                        align-items: center;
                        gap: 1rem;
                        text-align: center;
                        line-height: 20px;
                        letter-spacing: 1px;
                }
        }

</style>