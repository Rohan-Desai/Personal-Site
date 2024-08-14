<script setup>
import { onMounted } from '/vue'
import { gsap } from '/gsap'
import { MotionPathPlugin } from '/gsap/MotionPathPlugin'
import '@fortawesome/fontawesome-free/css/all.css'

gsap.registerPlugin(MotionPathPlugin)

onMounted(() => {
  gsap.from('.rohan-text', { duration: 1, opacity: 0, y: -50 })
  gsap.from('.desai-text', { duration: 1, opacity: 0, y: 50, delay: 1 })
  gsap.from('.swe-text', { duration: 1, opacity: 0, x: -100, delay: 2 })
  gsap.from('.icon', { duration: 1, opacity: 0, scale: 0, delay: 3 })
  gsap.from('.bouncing-circle', { duration: 1, opacity: 0, scale: 0, delay: 3 })

  gsap.to('.bouncing-circle', {
    y: -50,
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
      <div class="bouncing-circle"></div>
    </div>
    <div class="swe-text">
      <p>&lt;Software Engineer&gt;</p>
    </div>
    <div class="icons">
      <a href="https://github.com/Rohan-Desai" target="_blank" class="icon-link">
        <i class="fab fa-github icon"></i>
      </a>
      <a href="https://www.linkedin.com/in/rohan-desai-2a4b6b22a" target="_blank" class="icon-link">
        <i class="fab fa-linkedin icon"></i>
      </a>
      <a href="https://www.instagram.com" target="_blank" class="icon-link">
        <i class="fab fa-instagram icon"></i>
      </a>
      <a href="https://www.facebook.com" target="_blank" class="icon-link">
        <i class="fab fa-facebook icon"></i>
      </a>
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
  display: flex;
  align-items: flex-start; /* Align items to the top */
  padding-bottom: 100px;
}

.rohan-text,
.desai-text {
  font-family: 'Major Mono Display';
  color: white;
  font-size: 180px; /* Adjust font size relative to viewport width */
}

.rohan-text {
  position: relative;
  bottom: 100px;
  left: 100px;
}
.desai-text {
  position: relative;
  top: 100px;
  right: 100px;
}

.swe-text {
  font-family: 'Major Mono Display';
  font-style: italic;
  color: white;
  font-size: 25px;
  position: relative;
  bottom: 400px;
  left: 350px;
}

.icons {
  display: flex;
  flex-direction: row;
  gap: 25px;
  position: relative;
  top: 75px;
}

.icon {
  font-size: 80px;
  color: white;
}

.bouncing-circle {
  width: 15px;
  height: 15px;
  background-color: white;
  border-radius: 50%;
  position: relative;
  top: 175px;
  right: 175px;
}
/* Media queries for smaller screens */
@media (max-width: 1350px) {
  .rohan-text,
  .desai-text {
    font-size: 125px; /* Adjust font size relative to viewport width */
  }

  .rohan-text {
    bottom: 75px;
    left: 100px;
  }
  .desai-text {
    top: 75px;
    right: 100px;
  }

  .swe-text {
    font-size: 15px;
    bottom: 310px;
    left: 240px;
  }

  .icons {
    top: 100px;
  }

  .icon {
    font-size: 60px;
  }

  .bouncing-circle {
    top: 120px;
    right: 155px;
  }
}

/* Media queries for smaller screens */
@media (max-width: 940px) {
  .rohan-text,
  .desai-text {
    font-size: 75px; /* Adjust font size relative to viewport width */
  }

  .rohan-text {
    bottom: 50px;
    left: 50px;
  }
  .desai-text {
    top: 50px;
    right: 50px;
  }

  .swe-text {
    font-size: 10px;
    bottom: 230px;
    left: 150px;
  }

  .icons {
    top: 100px;
  }

  .icon {
    font-size: 40px;
  }

  .bouncing-circle {
    width: 10px;
    height: 10px;
    top: 75px;
    right: 85px;
  }
}

/* Media queries for very small screens */
@media (max-width: 570px) {
  .rohan-text,
  .desai-text {
    font-size: 50px; /* Adjust font size relative to viewport width */
  }

  .rohan-text {
    bottom: 40px;
    left: 25px;
  }
  .desai-text {
    top: 40px;
    right: 25px;
  }

  .swe-text {
    font-size: 8px;
    bottom: 190px;
    left: 100px;
  }

  .icons {
    top: 100px;
  }

  .icon {
    font-size: 30px;
  }

  .bouncing-circle {
    width: 5px;
    height: 5px;
    top: 59px;
    right: 47px;
  }
}

.flip-n,
.flip-s {
  display: inline-block;
  transform-origin: center;
}
</style>
