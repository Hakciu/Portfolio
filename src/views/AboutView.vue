<script setup>
  import test from '../components/test.vue'
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <test />
  </div>
</template>

<style>
  .about {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20rem 8rem 0 8rem;
  }
</style>
