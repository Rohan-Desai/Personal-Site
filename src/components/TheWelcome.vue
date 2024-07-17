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
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.name-wrapper {
  text-align: center;
}

.rohan-text,
.desai-text {
  font-family: 'Major Mono Display';
  color: white;
  font-size: 10vw; /* Adjust font size relative to viewport width */
}

.swe-text {
  font-family: 'Major Mono Display';
  font-style: italic;
  color: white;
  font-size: 3vw;
  margin-top: 2vh;
}

.icons {
  display: flex;
  flex-direction: row;
  gap: 2vw;
  margin-top: 5vh;
}

.icon {
  font-size: 5vw;
  color: white;
}

.bouncing-circle {
  width: 5vw;
  height: 5vw;
  background-color: white;
  border-radius: 50%;
  margin-top: 5vh;
}

/* Media queries for smaller screens */
@media (max-width: 768px) {
  .rohan-text,
  .desai-text {
    font-size: 15vw;
  }

  .swe-text {
    font-size: 5vw;
  }

  .icon {
    font-size: 8vw;
  }

  .bouncing-circle {
    width: 8vw;
    height: 8vw;
  }
}

/* Media queries for very small screens */
@media (max-width: 480px) {
  .rohan-text,
  .desai-text {
    font-size: 20vw;
  }

  .swe-text {
    font-size: 6vw;
  }

  .icon {
    font-size: 10vw;
  }

  .bouncing-circle {
    width: 10vw;
    height: 10vw;
  }
}

.flip-n,
.flip-s {
  display: inline-block;
  transform-origin: center;
}
</style>
