<script setup>
import LandingPage from './components/LandingPage.vue'
import SelfDescripton from './components/SelfDescription.vue'
import InterestPage from './components/InterestPage.vue'
import JobPage from './components/JobPage.vue'
import EducationPage from './components/EducationPage.vue'
</script>

<template>
  <main>
    <div class="landing-page">
      <LandingPage />
    </div>
    <div class="self-descripton-page">
      <SelfDescripton />
    </div>
    <div class="interest-page">
      <InterestPage />
    </div>
    <div class="job-page">
      <JobPage />
    </div>
    <div class="education-page">
      <EducationPage />
    </div>
  </main>
</template>

<style scoped>
.major-mono-display-regular {
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  font-style: normal;
}
/* .landing-page {
  height: 100vh;
}
.self-descripton-page {
  height: 400vh;
} */
.interest-page {
  height: 200vh;
}
.job-page {
  height: 300vh;
}
</style>
