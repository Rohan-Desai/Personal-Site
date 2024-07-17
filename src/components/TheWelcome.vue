<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { MotionPathPlugin } from 'gsap/MotionPathPlugin'
import '@fortawesome/fontawesome-free/css/all.css'

gsap.registerPlugin(MotionPathPlugin)

onMounted(() => {
  gsap.from('.rohan-text', { duration: 1, opacity: 0, y: -50 })
  gsap.from('.desai-text', { duration: 1, opacity: 0, y: 50, delay: 1 })
  gsap.from('.swe-text', { duration: 1, opacity: 0, x: -100, delay: 2 })
  gsap.from('.icon', { duration: 1, opacity: 0, scale: 0, delay: 3 })
  gsap.from('.bouncing-circle', { duration: 1, opacity: 0, scale: 0, delay: 3 })

  gsap.to('.bouncing-circle', {
    y: -80,
    duration: 0.5,
    yoyo: true,
    repeat: -1,
    ease: 'power1.inOut'
  })

  gsap.to('.flip-n', {
    rotationX: 720,
    duration: 2,
    repeat: -1,
    yoyo: true,
    ease: 'power1.inOut',
    delay: 1,
    repeatDelay: 2
  })
  gsap.to('.flip-s', {
    rotationY: 180,
    duration: 1,
    repeat: -1,
    yoyo: true,
    ease: 'power1.inOut',
    delay: 1.5,
    repeatDelay: 1
  })
})
</script>

<template>
  <div class="landing-page">
    <div class="name-wrapper">
      <div class="rohan-text">
        <p>Roha<span class="flip-n">n</span></p>
      </div>
      <div class="desai-text">
        <p>De<span class="flip-s">s</span>ai</p>
      </div>
    </div>
    <div class="swe-text">
      <p>&lt;Software Engineer&gt;</p>
    </div>
    <div class="bouncing-circle"></div>
    <div class="icons">
      <i class="fab fa-github icon"></i>
      <i class="fab fa-linkedin icon"></i>
      <i class="fab fa-instagram icon"></i>
      <i class="fab fa-facebook icon"></i>
    </div>
  </div>
</template>

<style scoped>
.landing-page {
  width: 100vw;
  height: 100vh;
}
.name-wrapper {
  position: absolute;
  margin-top: 100px;
  margin-left: -150px;
}

.rohan-text {
  font-family: 'Major Mono Display';
  font-size: 250px;
  height: 250px;
  color: white;
}

.desai-text {
  font-family: 'Major Mono Display';
  font-size: 250px;
  height: 250px;
  margin-left: 600px;
  color: white;
}

.swe-text {
  position: relative;
  font-family: 'Major Mono Display';
  font-style: italic;
  color: white;

  font-size: 30px;
  width: 500px;
  top: 300px;
  left: 850px;
}

.icons {
  display: flex;
  flex-direction: row;
  gap: 40px;
  position: absolute;
  top: 80%;
  left: 38.5%;
}

.icon {
  font-size: 80px;
  color: white;
}

.bouncing-circle {
  position: absolute;
  bottom: 52.5%;
  right: 9.5%;
  transform: translateX(-50%);
  width: 50px;
  height: 50px;
  background-color: white;
  border-radius: 50%;
}
.svg-container {
  top: 50%;
  position: absolute;
  z-index: auto;
  left: 20%;
}
.flip-n {
  display: inline-block;
  transform-origin: center;
}
.flip-s {
  display: inline-block;
  transform-origin: center;
}
</style>
