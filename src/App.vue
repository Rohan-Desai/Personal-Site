<script setup>
import LandingPage from './components/LandingPage.vue'
import SelfDescripton from './components/SelfDescription.vue'
import InterestPage from './components/InterestPage.vue'
import JobPage from './components/JobPage.vue'
</script>

<template>
  <main>
    <LandingPage />
    <SelfDescripton />
    <InterestPage />
    <JobPage />
  </main>
</template>

<style scoped>
.major-mono-display-regular {
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  font-style: normal;
}
</style>
