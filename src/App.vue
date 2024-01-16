<script setup>
  import { RouterView } from 'vue-router'
  import { ref, onMounted, onUnmounted, watch, provide } from 'vue'
  import Blob from './components/Blob.vue'
  import Blur from './components/Blur.vue'
  import Scrollbar from './components/Scrollbar.vue'
  import Navbar from './components/Navbar.vue'
  import Footer from './components/Footer.vue'

  import Lenis from '@studio-freight/lenis'
  let lenis
  let rafId

  const showNav = ref(false)
  const showPage = ref(false)
  const isLoading = ref(true)

  onMounted(() => {
    showPage.value = false
    lenis = new Lenis()

    const raf = (time) => {
      lenis.raf(time)
      rafId = requestAnimationFrame(raf)
    }

    rafId = requestAnimationFrame(raf)

    setTimeout(() => {
      isLoading.value = false
      showPage.value = true
    }, 2200)
  })

  provide('showPage', showPage)

  watch(showNav, (newVal) => {
    if (newVal) {
      lenis.stop()
    } else {
      lenis.start()
    }
  })

  const updateShowNav = (newVal) => {
    showNav.value = newVal
  }
</script>

<template>
  <div :class="!isLoading ? 'page-show' : 'page-hide'">
    <Navbar :showNav="showNav" @update:showNav="updateShowNav" />
    <div ref="container">
      <Scrollbar />
      <!-- <Blur /> -->
      <Blob />
      <RouterView v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </RouterView>
    </div>
    <Footer />
  </div>

  <div :class="isLoading ? 'loader' : 'done'">
    <div class="stage">
      <div class="dot-floating"></div>
    </div>
  </div>
</template>

<style scoped>
  .loader {
    position: fixed;
    top: 0;
    left: 0;
  }
  .done {
    display: none;
  }

  .page-hide {
    display: none;
  }
  .page-show {
    display: block;
  }

  .btn {
    position: absolute;
    top: 50;
    left: 50;
    z-index: 100;
  }
  .stage {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .dot-floating {
    position: relative;
    width: 5rem;
    height: 5rem;
    border-radius: 50%;
    background-color: #fbfbf6;
    color: #fbfbf6;
    animation: dot-floating 3s cubic-bezier(0.15, 0.6, 0.9, 0.1);
  }
  .dot-floating::before,
  .dot-floating::after {
    content: '';
    display: inline-block;
    position: absolute;
    top: 0;
  }
  .dot-floating::before {
    left: -6rem;
    width: 5rem;
    height: 5rem;
    border-radius: 50%;
    background-color: #a275ff;
    color: #a275ff;
    animation: dot-floating-before 3s ease-in-out;
  }
  .dot-floating::after {
    left: -12rem;
    width: 5rem;
    height: 5rem;
    border-radius: 50%;
    background-color: #fed075;
    color: #fed075;
    animation: dot-floating-after 3s cubic-bezier(0.4, 0, 1, 1);
  }

  @keyframes dot-floating {
    0% {
      left: calc(-50% - 65rem);
    }
    75% {
      left: calc(50% + 105rem);
    }
    100% {
      left: calc(50% + 105rem);
    }
  }
  @keyframes dot-floating-before {
    0% {
      left: -20rem;
    }
    50% {
      left: -6rem;
    }
    75% {
      left: -20rem;
    }
    100% {
      left: -20rem;
    }
  }
  @keyframes dot-floating-after {
    0% {
      left: -40rem;
    }
    50% {
      left: -12rem;
    }
    75% {
      left: -50rem;
    }
    100% {
      left: -50rem;
    }
  }
</style>
