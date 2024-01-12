<script setup></script>

<template>
  <footer>
    <div class="wave">
      <svg
        data-name="Layer 1"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 1200 120"
        preserveAspectRatio="none"
      >
        <path
          d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z"
          class="shape-fill"
        ></path>
      </svg>
    </div>
    <p>2024 © Jakub Janik</p>
    <div class="routes">
      <router-link to="/work">Work</router-link>
      <router-link to="/about">About</router-link>
      <router-link to="/contact">Contact</router-link>
    </div>
    <a class="mail" href="mailto:JJanik2k@gmail.com">JJanik2k@gmail.com</a>
  </footer>
</template>

<style scoped>
  .wave {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    overflow: hidden;
    line-height: 0;
    transform: rotate(180deg);
  }

  .wave svg {
    position: relative;
    display: block;
    width: calc(292% + 1.3px);
    height: 25rem;
  }

  .wave .shape-fill {
    fill: #a275ff;
  }

  footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 10rem;
    padding: 1rem 8rem;
    padding-bottom: 3rem;
    color: #1c1d1e;
  }

  .routes {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  p,
  .mail {
    font-size: 1.2rem;
    font-weight: normal !important;
  }

  a {
    color: #1c1d1e;
    text-decoration: none;
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0 1rem;
    transition: color 0.2s ease-in-out;
  }

  a:hover {
    color: #fbfbf6;
  }
</style>
