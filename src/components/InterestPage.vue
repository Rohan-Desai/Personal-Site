<script setup>
import { ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { onMounted, onBeforeUnmount } from 'vue'

gsap.registerPlugin(ScrollTrigger)

const section1 = ref(null)
const section2 = ref(null)
const section3 = ref(null)
const section4 = ref(null)
const line = ref(null)
const circles = ref([])

onMounted(() => {
  ScrollTrigger.create({
    trigger: '.scroll-container',
    start: 'top top',
    end: 'bottom bottom',
    scrub: true,
    pin: true,
    id: 'myScrollTrigger',
    onUpdate: (self) => {
      const progress = self.progress
      gsap.to(line.value, {
        backgroundImage: `linear-gradient(to bottom, white ${progress * 135}%, black ${progress * 100}%)`
      })

      if (progress < 0.25) {
        gsap.to(section1.value, { autoAlpha: 1 })
        gsap.to(section2.value, { autoAlpha: 0 })
        gsap.to(section3.value, { autoAlpha: 0 })
        gsap.to(section4.value, { autoAlpha: 0 })
        gsap.to(circles.value[0], { backgroundColor: 'white' })
        gsap.to(circles.value.slice(1), { backgroundColor: 'black' })
      } else if (progress < 0.5) {
        gsap.to(section1.value, { autoAlpha: 0 })
        gsap.to(section2.value, { autoAlpha: 1 })
        gsap.to(section3.value, { autoAlpha: 0 })
        gsap.to(section4.value, { autoAlpha: 0 })
        gsap.to([circles.value[0], circles.value[1]], { backgroundColor: 'white' })
        gsap.to([circles.value[2], circles.value[3]], {
          backgroundColor: 'black'
        })
      } else if (progress < 0.75) {
        gsap.to(section1.value, { autoAlpha: 0 })
        gsap.to(section2.value, { autoAlpha: 0 })
        gsap.to(section3.value, { autoAlpha: 1 })
        gsap.to(section4.value, { autoAlpha: 0 })
        gsap.to([circles.value[0], circles.value[1], circles.value[2]], {
          backgroundColor: 'white'
        })
        gsap.to([circles.value[3]], {
          backgroundColor: 'black'
        })
      } else {
        gsap.to(section1.value, { autoAlpha: 0 })
        gsap.to(section2.value, { autoAlpha: 0 })
        gsap.to(section3.value, { autoAlpha: 0 })
        gsap.to(section4.value, { autoAlpha: 1 })
        gsap.to([circles.value[0], circles.value[1], circles.value[2], circles.value[3]], {
          backgroundColor: 'white'
        })
      }
    }
  })
  ScrollTrigger.refresh()
})
onBeforeUnmount(() => {
  ScrollTrigger.getAll().forEach((trigger) => trigger.kill())
})
const pages = ref([
  { text: 'Page 1 content text', image: 'path/to/image1.jpg' },
  { text: 'Page 2 content text', image: 'path/to/image2.jpg' },
  { text: 'Page 3 content text', image: 'path/to/image3.jpg' },
  { text: 'Page 4 content text', image: 'path/to/image4.jpg' }
])
</script>

<template>
  <div class="scroll-container">
    <div ref="section1" class="section">
      <div class="audio-content">
        <audio controls>
          <source src="/src/assets/almostrain.m4a" type="audio/mpeg" />
          Your browser does not support the audio tag.
        </audio>

        <audio controls>
          <source src="/src/assets/FACGCE.m4a" type="audio/mpeg" />
          Your browser does not support the audio tag.
        </audio>

        <audio controls>
          <source src="/src/assets/RocketShip.m4a" type="audio/mpeg" />
          Your browser does not support the audio tag.
        </audio>

        <audio controls>
          <source src="/src/assets/Yurr.m4a" type="audio/mpeg" />
          Your browser does not support the audio tag.
        </audio>
      </div>
      <div class="text-content">
        <div class="heading-text right1">
          <p>pRoducTioN</p>
        </div>
        <div class="body-text right1">
          <p>
            each track i produce, whether on guitar, piano, drums, or bass, showcases the beautiful
            interplay of physics and mathematics—foundational elements that make music both possible
            and profound. my journey through various musical landscapes is not just about
            innovation, but also a deep appreciation of the intricate craftsmanship behind every
            note.
          </p>
        </div>
      </div>
    </div>
    <div ref="section2" class="section">
      <div class="text-content">
        <div class="heading-text left2">
          <p>dANCe</p>
        </div>
        <div class="body-text left2">
          <p>
            dance is a powerful expression of cultural identity and personal creativity. my
            exploration of different dance styles serves as a vibrant bridge to my indian roots.
            this pursuit integrates with my cognitive science background, providing insights into
            the neural and psychological aspects of movement and rhythm.
          </p>
        </div>
      </div>
      <div class="media-content">
        <iframe
          class="youtube-video right2"
          src="https://www.youtube.com/embed/UF12Nmh-_W8?si=GVABVhLtqEzVjidp&t=4409"
          title="YouTube video player"
          frameborder="0"
          allow="accelerometer; gyroscope;"
          allowfullscreen
          loading="lazy"
        >
        </iframe>
      </div>
    </div>
    <div ref="section3" class="section">
      <div class="media-content">
        <iframe
          class="youtube-video left1"
          src="https://www.youtube.com/embed/IPvJzeskL10?si=jqDWps0OkLFd1C88"
          title="YouTube video player"
          frameborder="0"
          allow="accelerometer; gyroscope;"
          allowfullscreen
          loading="lazy"
        >
        </iframe>
      </div>
      <div class="text-content">
        <div class="heading-text right1">
          <p>yOGA/MEDiTATiON</p>
        </div>
        <div class="body-text right1">
          <p>
            yoga and meditation are foundational practices that keep me grounded and mentally clear,
            particularly valuable in the demanding fields of computer science and cognitive science.
            embracing these practices at the start and end of each day promotes a balanced mind and
            body, enhancing focus and productivity.
          </p>
        </div>
      </div>
    </div>
    <div ref="section4" class="section">
      <div class="text-content">
        <div class="heading-text left2">
          <p>MisceLLANeous</p>
        </div>
        <div class="body-text left2">
          <p>
            as a tennis enthusiast, i enjoy the game's strategic challenges. i discuss cutting-edge
            tech, showcasing my commitment to innovation. ny interests in economics and cognitive
            science explore market nuances and decision-making. playing guitar enriches my
            creativity and highlights the connection between music and math.
          </p>
        </div>
      </div>
      <div class="media-content">
        <iframe
          class="youtube-video right2"
          src="https://youtube.com/embed/7dx93nuWz58"
          title="YouTube video player"
          frameborder="0"
          allow="accelerometer; gyroscope;"
          allowfullscreen
          loading="lazy"
        >
        </iframe>
      </div>
    </div>
    <div class="scroll-tracker">
      <div ref="line" class="line"></div>
      <div
        v-for="(page, index) in pages"
        :key="index"
        ref="circles"
        class="circle"
        :style="{ top: `${index * 33}%` }"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.scroll-container {
  height: 200vh; /* Example height, adjust as needed */
  position: relative;
}

.section {
  height: 100vh; /* Each section takes full viewport height */
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
  opacity: 0;
}

.section:nth-child(1) {
  background-image: linear-gradient(#63b4ff, #d0e9ff);
}

.section:nth-child(2) {
  background-image: linear-gradient(#ff63d3, #ffd5f3);
}

.section:nth-child(3) {
  background-image: linear-gradient(#ff6c6c, #ffd2d2);
}
.section:nth-child(4) {
  background-image: linear-gradient(#ffae63, #ffecda);
}

.scroll-tracker {
  position: relative;
  width: 40px;
  height: 30%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 22vh;
  left: 47vw;
}

.line {
  width: 2px;
  height: 100%;
  margin-left: 75px;
  margin-right: 75px;
  background-color: black;
}

.circle {
  width: 20px;
  height: 20px;
  background-color: black;
  border-radius: 50%;
  position: absolute;
}
.audio-content {
  position: relative;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin-bottom: 10px;
  width: 39vw;
  height: 40vh;
  top: 33vh;
  left: 5vw;
}

audio {
  width: 100%;
}
.right1 {
  position: relative;
  width: 39vw;
  left: 52vw;
  bottom: 11vh;
  align-content: left;
}
.heading-text {
  font-family: 'Major Mono Display';
  color: black;
  font-size: 3vw;
}

.body-text {
  font-family: 'Major Mono Display';
  color: black;
  font-size: 1.1vw;
  align-items: left;
  margin-left: 2px;
}
.left1 {
  position: relative;
  width: 39vw;
  height: 40vh;
  margin: 0 auto;
  top: 31vh;
  left: 5vw;
}

.right2 {
  position: relative;
  width: 39vw;
  height: 40vh;
  left: 54vw;
  bottom: 3vh;
  align-content: left;
}

.left2 {
  position: relative;
  width: 39vw;
  top: 30vh;
  left: 4vw;
}
.youtube-video {
  border: none;
}

@media (min-width: 2400px) {
  .right2 {
    top: 3vh;
  }
  .heading-text {
    font-size: 3vw;
  }
  .body-text {
    font-size: 1.1vw;
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
  .right2 {
    bottom: 2.5vh;
  }
  .heading-text {
    font-size: 3vw;
  }
  .body-text {
    font-size: 1.1vw;
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .right2 {
    top: 2vh;
  }
  .heading-text {
    font-size: 3vw;
  }
  .body-text {
    font-size: 1.1vw;
  }
}
@media (max-width: 1380px) and (min-width: 850px) {
  .heading-text {
    font-size: 4vw;
  }
  .body-text {
    font-size: 1.4vw;
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .right2 {
    top: 4vh;
  }
  .heading-text {
    font-size: 4vw;
  }
  .body-text {
    font-size: 1.5vw;
  }
}
@media (max-width: 500px) {
  .right2 {
    top: 5vh;
  }
  .heading-text {
    font-size: 5vw;
  }
  .body-text {
    font-size: 2vw;
  }
}
</style>
