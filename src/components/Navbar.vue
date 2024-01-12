<script setup>
  import { ref, reactive, onMounted, watch, inject } from 'vue'
  import Logo from './Logo.vue'
  import Lenis from '@studio-freight/lenis'

  const lenisInstance = new Lenis()

  const props = defineProps({
    showNav: Boolean,
  })

  const emit = defineEmits(['update:showNav'])

  const hover = ref(false)
  const hoverDelay = ref(0)
  const extraColors = reactive(['#fed075', 'rgb(96, 137, 92)', '#a275ff'])

  const updateHoverDelay = () => {
    if (hover.value) {
      if (hoverDelay.value < extraColors.length) {
        hoverDelay.value++
      }
    } else {
      hoverDelay.value = 0
    }
  }

  onMounted(() => {
    setInterval(updateHoverDelay, 100)
  })

  const toggleNav = () => {
    emit('update:showNav', !props.showNav)
  }

  watch(
    () => props.showNav,
    (newVal) => {
      if (newVal) {
        extraColors.push('#fbfbf6')
        lenisInstance.stop()
      } else {
        const index = extraColors.indexOf('#fbfbf6')
        if (index !== -1) {
          extraColors.splice(index, 1)
        }
        lenisInstance.start()
      }
    }
  )

  const show = inject('showPage')

  const showMail = ref(false)
</script>

<template>
  <nav>
    <Transition name="scale">
      <Logo :showNav="showNav" v-if="show" />
    </Transition>
    <Transition name="scale">
      <div class="menu" v-if="show">
        <div
          class="hamburger"
          :class="{ hamburger2: showNav }"
          @mouseover="hover = true"
          @mouseleave="hover = false"
          @click="toggleNav"
        >
          <div class="hamburger-line" :class="{ X1: showNav }"></div>
          <div class="hamburger-line" :class="{ hideLine: showNav }"></div>
          <div class="hamburger-line" :class="{ X2: showNav }"></div>
          <div
            class="extra-color"
            v-for="(color, index) in extraColors"
            :class="{ show: hover && index < hoverDelay }"
            :style="{ background: color }"
          ></div>
        </div>
      </div>
    </Transition>

    <div
      class="white-container"
      :class="{ show: showNav }"
      :style="{
        transform: showNav ? 'translate(0, 0)' : 'translate(0, -100%)',
      }"
    >
      <div class="mail-area" :style="{ opacity: showNav ? '1' : '0' }">
        <p>Get in touch</p>
        <h4 class="mail">JJanik2k@gmail.com</h4>
      </div>
      <div class="routes">
        <h2 data-text="work" class="work">work</h2>
        <h2 data-text="about me" class="about-me">about me</h2>
        <h2 data-text="contact" class="contact">contact</h2>
      </div>
    </div>
  </nav>
</template>

<style>
  nav {
    position: relative;
    z-index: 4;
  }

  .hideLine {
    opacity: 0;
  }

  .X1 {
    transform: rotate(45deg);
    top: 0.55rem;
    background-color: #1c1d1e !important;
  }

  .X2 {
    transform: rotate(-45deg);
    top: -0.55rem;
    background-color: #1c1d1e !important;
  }

  .menu {
    position: fixed;
    z-index: 5;
    width: 100%;
    transform-origin: right;
  }

  .hamburger2 {
    background-color: transparent !important;
    border: 1px solid #1c1d1e !important;
  }

  .hamburger {
    position: fixed;
    right: 2rem;
    top: 2rem;
    z-index: 5;
    background-color: #a275ff;
    padding: 1.5rem;
    border-radius: 50%;
    cursor: pointer;
    overflow: hidden;
    color: rgb(96, 137, 92);
    transition: background-color 0.3s ease-in-out;
  }

  .hamburger::before,
  .hamburger::after,
  .hamburger span::before,
  .hamburger span::after {
    content: '';
  }

  .extra-color {
    content: '';
    position: absolute;
    top: 50%;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    transform: scale(0);
    transition: transform 0.2s;
    visibility: hidden;
  }

  .extra-color.show {
    transform: scale(2);
    visibility: visible;
    animation: scaleUp 0.2s forwards;
  }

  .hamburger-line {
    width: 30px;
    height: 3px;
    background-color: #fbfbf6;
    margin: 6px 0;
    transition: 0.4s;
    border-radius: 5px;
    z-index: 5;
  }

  .white-container {
    position: fixed;
    width: 100vw;
    height: 100vh;
    background-color: #fbfbf6;
    top: 0;
    left: 0;
    transform: translate(0, -200%);
    transition: all 0.3s ease-in-out;
    z-index: 4;
    border-radius: 0 0 50% 50%;
    color: #1c1d1e;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .white-container.show {
    border-radius: 0;
  }

  .routes {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: 'Lilita One', sans-serif;
  }

  h2 {
    font-size: 8rem;
    cursor: pointer;
    font-family: 'Konkhmer Sleokchher', system-ui;
    position: relative;
  }

  h2 {
    box-shadow: inset 0 0 0 0 #1c1d1e;
    padding: 0 0.25rem;
    margin: 0 -0.25rem;
    transition: color 0.5s ease-in-out, box-shadow 0.5s ease-in-out;
    padding: 0 2rem;
  }

  h2:hover {
    color: #fbfbf6;
    box-shadow: inset 41rem 0 0 0 #1c1d1e;
  }

  .mail-area {
    position: absolute;
    bottom: 0;
    left: 0;
    padding: 2rem;
    font-family: 'Poppins', sans-serif;
    font-size: 1.4rem;
    transition: opacity 0.2s ease;
  }

  .mail-area p {
    color: #a275ff;
  }

  .mail {
    font-size: 2rem;
  }
</style>
