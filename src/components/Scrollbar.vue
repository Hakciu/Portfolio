<template>
  <div id="scrollBar" ref="scrollBar"></div>
</template>

<script setup>
  import { onMounted, ref } from 'vue'

  const scrollBar = ref(null)

  onMounted(() => {
    let scrollTimeout = null

    window.onscroll = function () {
      clearTimeout(scrollTimeout)

      var winScroll =
        document.body.scrollTop || document.documentElement.scrollTop
      var height =
        document.documentElement.scrollHeight -
        document.documentElement.clientHeight
      var scrolled = (winScroll / height) * 85
      scrollBar.value.style.height = '15vh'
      scrollBar.value.style.top = scrolled + '%'
      scrollBar.value.style.opacity = '1'

      scrollTimeout = setTimeout(() => {
        scrollBar.value.style.opacity = '0'
      }, 1000)
    }
  })
</script>

<style scoped>
  #scrollBar {
    position: fixed;
    top: 0;
    right: 0;
    width: 10px;
    height: 15vh;
    background: #a275ff;
    border-radius: 5px;
    opacity: 0;
    transition: height 0.3s, opacity 0.5s; /* Dodano transition dla opacity */
  }
</style>
