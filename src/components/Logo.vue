<script setup>
  import { ref, watch, onMounted, onUnmounted } from 'vue'

  const props = defineProps(['showNav'])

  const textColor = ref('')
  const past70vh = ref(false)

  watch(
    () => props.showNav,
    (newVal) => {
      textColor.value = newVal ? '#1c1d1e' : '#fbfbf6'
    }
  )

  const text = ref(false)
  const letters = ['H', 'a', 'k', 'e', 'n']
  const letterStyles = ref(
    letters.map((_, index) => ({
      transform: 'translateX(0px) rotate(0deg)',
      opacity: 1,
    }))
  )
  const svgStyle = ref({
    opacity: 0,
    transform: 'translateX(-1rem) rotate(-30deg)',
    transition:
      'transform 0.7s cubic-bezier(0.47, 1.64, 0.41, 0.8), opacity 0.3s ease',
  })

  const toggleText = () => {
    text.value = !text.value
    // Aktualizacja stylów dla liter
    letterStyles.value = letterStyles.value.map((_, index) => {
      const moveX = text.value ? -1.3 * (index + 1) : 0
      const rotate = text.value ? -10 * (index + 1) : 0
      const opacity = text.value ? 0 : 1
      return {
        transform: `translateX(${moveX}rem) rotate(${rotate}deg)`,
        opacity: opacity,
      }
    })
    // Aktualizacja stylu SVG
    svgStyle.value.opacity = text.value ? 1 : 0
    svgStyle.value.transform = text.value
      ? 'translateX(1rem) rotate(0deg)'
      : 'translateX(-1rem) rotate(-30deg)'
  }

  onMounted(() => {
    window.addEventListener('scroll', () => {
      if (window.scrollY > 0.7 * window.innerHeight && !past70vh.value) {
        past70vh.value = true
        toggleText()
      } else if (window.scrollY <= 0.7 * window.innerHeight && past70vh.value) {
        past70vh.value = false
        toggleText()
      }
    })
  })

  onUnmounted(() => {
    window.removeEventListener('scroll', toggleText)
  })
</script>

<template>
  <main>
    <router-link to="/">
      <div class="text" :style="{ color: textColor }">
        <span
          class="letter"
          v-for="(letter, index) in letters"
          :key="index"
          :style="letterStyles[index]"
          >{{ letter }}</span
        >
      </div>
    </router-link>
    <router-link to="/">
      <svg
        :style="svgStyle"
        width="82.40007324218749px"
        height="122px"
        class="svg-animation"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="208.79996337890626 14 82.40007324218749 122"
        preserveAspectRatio="xMidYMid"
      >
        <defs>
          <filter
            id="editing-extrusion"
            x="-100%"
            y="-100%"
            width="300%"
            height="300%"
          >
            <feFlood result="color1" flood-color="#444"></feFlood>
            <feConvolveMatrix
              order="8,8"
              divisor="1"
              kernelMatrix="1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1"
              in="SourceAlpha"
              result="extrude"
            ></feConvolveMatrix>
            <feComposite
              in="color1"
              in2="extrude"
              result="comp-extrude"
              operator="in"
            ></feComposite>
            <feOffset
              dx="4"
              dy="4"
              in="comp-extrude"
              result="offset-extrude"
            ></feOffset>
            <feMerge>
              <feMergeNode in="offset-extrude"></feMergeNode>
              <feMergeNode in="SourceGraphic"></feMergeNode>
            </feMerge>
          </filter>
        </defs>
        <g filter="url(#editing-extrusion)">
          <g transform="translate(227.72710904479027, 96.76000022888184)">
            <path
              d="M24.96-4.80L24.96-4.80L24.96-4.80Q24.96-9.28 26.75-18.24L26.75-18.24L17.28-18.24L13.76 0L0.38 0L8.51-42.24L22.02-42.24L18.30-23.36L27.78-23.36L31.30-42.24L44.80-42.24L44.80-42.24Q43.90-37.50 42.75-32.19L42.75-32.19L40.58-21.76L40.58-21.76Q38.14-9.60 38.14-4.29L38.14-4.29L38.14-4.29Q38.14-2.11 38.85-0.90L38.85-0.90L38.85-0.90Q35.65 1.28 31.90 1.28L31.90 1.28L31.90 1.28Q28.16 1.28 26.56-0.51L26.56-0.51L26.56-0.51Q24.96-2.30 24.96-4.80Z"
              fill="#ccc"
              data-darkreader-inline-fill=""
              style="--darkreader-inline-fill: #35393b"
            ></path>
          </g>
        </g>
      </svg>
    </router-link>
  </main>
</template>

<style scoped>
  svg {
    transition: transform 0.3s cubic-bezier(0.47, 1.64, 0.41, 0.8),
      opacity 0.3s ease;
  }

  svg {
    position: absolute;
    top: 0;
    left: 0;
  }

  .text {
    position: absolute;
    top: 1.5rem;
    left: 2rem;
    display: flex;
    color: #fbfbf6;
    font-family: 'Bungee', sans-serif;
    transition: color 0.5s ease;
  }

  main {
    position: fixed !important;
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 110;
  }

  .text {
    font-size: 3rem;
    z-index: 10;
  }
  .letter {
    display: inline-block;
    transition: transform 0.7s cubic-bezier(0.47, 1.64, 0.41, 0.8),
      opacity 0.3s ease;
  }
</style>
