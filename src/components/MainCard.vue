<template>
  <main>
    <img
      src="https://www.gifcen.com/wp-content/uploads/2022/05/black-hole-gif-1.gif"
      width="600"
      height="600"
      alt="Description of the image"
      ref="tiltElement"
    />
  </main>
</template>

<script setup>
  import { onMounted, ref } from 'vue'
  import VanillaTilt from 'vanilla-tilt'

  let tiltElement = ref(null)

  onMounted(() => {
    VanillaTilt.init(tiltElement.value, {
      max: 10,
      speed: 20,
      perspective: 500,
      'full-page-listening': true,
      reverse: true,
      reset: false,
    })
  })
</script>

<style scoped>
  img {
    border-radius: 50px;
  }
</style>
