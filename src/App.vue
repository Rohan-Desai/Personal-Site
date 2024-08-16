<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import LandingPage from './components/LandingPage.vue';
import SelfDescripton from './components/SelfDescription.vue';
import InterestPage from './components/InterestPage.vue';
import JobPage from './components/JobPage.vue';
import EducationPage from './components/EducationPage.vue';
import ProjectPage from './components/ProjectPage.vue';
import SkillsPage from './components/SkillsPage.vue';

const isSmallScreen = ref(false);

const checkScreenSize = () => {
  isSmallScreen.value = window.innerWidth < 768;
};

onMounted(() => {
  checkScreenSize();
  window.addEventListener('resize', checkScreenSize);
});

onUnmounted(() => {
  window.removeEventListener('resize', checkScreenSize);
});
</script>

<template>
  <main v-if="!isSmallScreen">
    <div class="landing-page">
      <LandingPage />
    </div>
    <div class="self-descripton-page">
      <SelfDescripton />
    </div>
    <div class="education-page">
      <EducationPage />
    </div>
    <div class="job-page">
      <JobPage />
    </div>
    <div class="project-page">
      <ProjectPage />
    </div>
    <div class="interest-page">
      <InterestPage />
    </div>
    <div class="skills-page">
      <SkillsPage />
    </div>
  </main>
  <div v-else class="small-screen-warning">
    This website is only meant for screen sizes 768 pixels and above.
  </div>
</template>

<style scoped>
html {
  scroll-behavior: smooth;
}

.major-mono-display-regular {
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  font-style: normal;
}

.interest-page {
  height: 200vh;
}

.job-page {
  height: 200vh;
}

.small-screen-warning {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: red;
  color: white;
  font-size: 18px;
  text-align: center;
  z-index: 1000;
}
</style>
