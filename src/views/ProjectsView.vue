<script setup>
  import test from '@/components/test.vue'
</script>

<template>
  <div class="projects">
    <h1>This is an projects page</h1>
    <test />
  </div>
</template>

<style>
  .projects {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20rem 8rem 0 8rem;
  }
</style>
