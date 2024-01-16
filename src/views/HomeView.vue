<script setup>
  import MainCard from '../components/MainCard.vue'
  import test from '../components/test.vue'

  import { inject } from 'vue'
  const show = inject('showPage')
</script>

<template>
  <div>
    <main>
      <Transition name="scale">
        <div class="main-card" v-if="show">
          <!-- <MainCard /> -->

          <h1 class="hero">Lorem</h1>
        </div>
      </Transition>
      <div class="empty-space"></div>
    </main>
    <test />
  </div>
</template>

<style scoped>
  .main-card {
    transform-origin: bottom;
  }
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .hero {
    font-size: 20rem;
    font-weight: 900;
    color: #fbfbf6;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 4;
    font-family: 'Lexend', sans-serif;
  }
</style>
