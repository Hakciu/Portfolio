<script setup>
  import { ref, onMounted, onUnmounted } from 'vue'

  const blobStyle = ref({
    top: '50%',
    left: '50%',
    position: 'absolute',
    transform: 'translate(-50%, -50%)',
  })

  let targetX = window.innerWidth / 2
  let targetY = window.innerHeight / 2
  let currentX = targetX
  let currentY = targetY

  const updateBlobPosition = () => {
    const dx = targetX - currentX
    const dy = targetY - currentY
    currentX += dx * 0.04 - 8 // Tu możesz dostosować szybkość ruchu
    currentY += dy * 0.04 - 8 // Tu możesz dostosować szybkość ruchu

    blobStyle.value.left = `${currentX}px`
    blobStyle.value.top = `${currentY}px`

    requestAnimationFrame(updateBlobPosition)
  }

  onMounted(() => {
    window.addEventListener('mousemove', (e) => {
      targetX = e.clientX
      targetY = e.clientY
    })

    requestAnimationFrame(updateBlobPosition)
  })

  onUnmounted(() => {
    window.removeEventListener('mousemove', updateBlobPosition)
  })
</script>

<template>
  <div class="fixed-blob">
    <svg
      id="visual"
      viewBox="0 0 600 600"
      width="600"
      height="600"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      version="1.1"
      :style="blobStyle"
    >
      <defs>
        <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" style="stop-color: rgb(76, 230, 178)" />
          <stop offset="100%" style="stop-color: mediumpurple" />
        </linearGradient>
      </defs>
      <g transform="translate(311.5018511713091 337.0876494332855)">
        <path id="changePath" fill="url(#gradient)"></path>
      </g>
    </svg>
  </div>
</template>

<style scoped>
  @keyframes changePath {
    0%,
    100% {
      d: path(
        'M141 -213.7C179.6 -165.9 205.8 -120.7 229.3 -69.5C252.7 -18.4 273.3 38.5 269.5 99.1C265.7 159.7 237.5 223.8 188.5 247C139.5 270.1 69.8 252.3 10.5 237.8C-48.8 223.4 -97.6 212.4 -148.1 189.8C-198.7 167.2 -251 132.9 -275.3 83.5C-299.6 34.1 -295.8 -30.4 -282 -97.4C-268.1 -164.4 -244.3 -233.9 -195.6 -278.4C-146.9 -322.9 -73.5 -342.5 -11.2 -327.1C51.1 -311.7 102.3 -261.4 141 -213.7'
      );
    }
    50% {
      d: path(
        'M183.3 -240.4C231.8 -217.1 261.4 -155.8 265.6 -97.1C269.8 -38.4 248.5 17.7 229.4 73.9C210.3 130.1 193.3 186.4 155.4 236.6C117.6 286.8 58.8 330.9 5.2 323.8C-48.4 316.6 -96.8 258.2 -151.5 213.5C-206.2 168.8 -267.1 137.7 -299.7 85.9C-332.2 34.2 -336.4 -38.2 -308.7 -93.2C-281.1 -148.2 -221.6 -185.7 -164.9 -206.4C-108.2 -227 -54.1 -230.7 6.7 -239.9C67.4 -249 134.8 -263.7 183.3 -240.4'
      );
    }
  }

  #changePath {
    animation: changePath 6s infinite;
  }

  @keyframes rotate {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  svg {
    animation: rotate 30s linear infinite;
  }

  .fixed-blob {
    position: fixed;
    z-index: -1;
  }
</style>
