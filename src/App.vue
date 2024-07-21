<script setup>
import LandingPage from './components/LandingPage.vue'
import SelfDescripton from './components/SelfDescription.vue'
import InterestPage from './components/InterestPage.vue'
</script>

<template>
  <main>
    <LandingPage />
    <SelfDescripton />
    <InterestPage />
  </main>
</template>

<style scoped>
.major-mono-display-regular {
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  font-style: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
