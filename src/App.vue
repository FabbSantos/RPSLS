<script setup>
import Game from './components/Game.vue';
import Footer from './components/Footer.vue';
import { onMounted, provide, ref } from 'vue';


let score = ref(0);
provide('score', score);

onMounted(() => {
  const h1 = document.querySelector('h1');
  if (h1) {
    h1.innerHTML = h1.textContent.trim().split(' ').map(part => `<span>${part.trim()}</span>`).join('');
  }
});
</script>

<template>
  <header>
    <div class="headeboard">
        <h1>
          Rock Papers Scissors Lizard Spock
        </h1>

        <div class="score">
          <p>score</p>
          <p> {{score}} </p>
        </div>
    </div>
  </header>

  <main>
    <Game/>
  </main>

  <Footer />
</template>

<style scoped>
  main {
    width: 100%;
  }
  .headeboard {
    border: 5px solid var(--header-outline);
    border-radius: calc(var(--border-radius) + 10px);
    padding: 1.5rem;
    min-width: 52svw;
    color: white;
    text-align: center;
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-transform: uppercase;
  }
  h1 {
    font-size: clamp(1rem, 2.3vw, 2.5rem);
    line-height: 32px;
    font-weight: 700;
    text-align: left;
  }
  h1 > *{
    display: inline-block;
    width: 100%;
    font-weight: inherit;

  }
  .score {
    --min-width: 80px;
    background-color: white;
    box-shadow: 0 0 10px 2px var(--header-outline);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: clamp(1rem, 1vw, 1rem);
    font-weight: 700;
    min-width: var(--min-width);
    padding: 1rem;
    padding-inline: calc(var(--min-width) - 2rem);
    aspect-ratio: 2 / 1;
    border-radius: var(--border-radius);
    letter-spacing: 3px;
  }
  .score > p {
    color: var(--score-text);
    font-weight: 600;
  }
  .score > p:nth-of-type(2) {
    font-size: clamp(2rem, 3vw, 5rem);
    font-weight: inherit;
    color: var(--dark-text);
    line-height: 1.1;
  }

  @media (max-width: 768px){
    .score {
          --min-width: 50px;
          letter-spacing: 1px;
    }
    .headeboard {
      gap: 2rem;
    }
    header {
        width: 90%;
    }
    
    h1 {
      display: flex;
      flex-direction: column;
      align-items: center;
      line-height: 15px;
    }
  }
</style>
