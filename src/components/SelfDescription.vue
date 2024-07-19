<script setup>
import { onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const panels = gsap.utils.toArray('.content .panel')
    gsap.to('.content', {
      x: () => -window.innerWidth * (panels.length - 1),
      ease: 'none',
      scrollTrigger: {
        trigger: '.wrapper',
        start: 'top top',
        end: '+=' + window.innerWidth * (panels.length - 1),
        scrub: true,
        invalidateOnRefresh: false,
        pin: true
      }
    })

    // Adding rotation animation for stars
    gsap.utils.toArray('.star').forEach((star) => {
      gsap.to(star, {
        rotation: 360,
        ease: 'none',
        scrollTrigger: {
          trigger: '.wrapper',
          start: 'top top',
          end: '+=3000', // Adjust this value based on the length of your scroll
          scrub: true
        }
      })
    })
  })
})

onUnmounted(() => {
  ctx && ctx.revert()
})
</script>

<template>
  <div class="section wrapper">
    <div class="content">
      <div id="panel1" class="panel center">
        <div class="top-stars">
          <div class="star bluestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
          <div class="star whitestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
          <div class="star purplestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
        </div>
        <h1>
          <span class="boxed bluebox">adapting</span> at
          <span class="boxed purplebox">all times</span>
        </h1>
        <div class="bottom-stars">
          <div class="star bluestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
          <div class="star whitestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
          <div class="star purplestar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path
                d="M12 2l2.09 6.26H20.18l-5.45 3.96 2.09 6.26L12 14.52l-5.45 3.96 2.09-6.26-5.45-3.96h6.09L12 2z"
              />
            </svg>
          </div>
        </div>
      </div>
      <div id="panel2" class="panel center">
        <h1>carving my own path</h1>
      </div>
      <div id="panel3" class="panel center">
        <h1>pushing the status quo</h1>
      </div>
      <div id="panel4" class="panel center">
        <h1>Exploring The Unknown</h1>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 100%;
  background-color: var(--color-background);
  overflow: hidden;
}

.content {
  height: 100vh;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
}

.panel {
  flex: 1 0 100vw;
  color: var(--dark);
  font-family: 'Major Mono Display';
  color: white;
  font-size: 2.6vw;
  justify-content: center;
  align-items: center;
}

h1 {
  padding-left: 100px;
  padding-right: 100px;
}
.boxed {
  border: 1px solid white;
  border-radius: 15px;
  padding: 0 10px;
  margin: 0 5px;
  display: inline-block;
  box-sizing: border-box;
}
.bluebox {
  background-color: #63b4ff;
}
.purplebox {
  background-color: #b163ff;
}

.top-stars {
  display: flex;
  justify-content: space-around;
  width: 100%;
  padding-bottom: 20px;
}

.bottom-stars {
  display: flex;
  justify-content: space-around;
  width: 100%;
  padding-top: 20px;
}

.star {
  width: 300px;
  height: 300px;
}
.star svg {
  width: 100%;
  height: 100%;
}
.bluestar {
  fill: #63b4ff;
}
.whitestar {
  fill: #fff;
}
.purplestar {
  fill: #b163ff;
}

@media (max-width: 1380px) {
  .panel {
    font-size: 2.2vw;
  }
  .star {
    width: 200px;
    height: 200px;
  }
}
@media (max-width: 850px) {
  .panel {
    font-size: 2vw;
  }
  .star {
    width: 150px;
    height: 150px;
  }
}
@media (max-width: 700px) {
  .panel {
    font-size: 1.9vw;
  }
  .star {
    width: 50px;
    height: 50px;
  }
  h1 {
    padding-left: 50px;
    padding-right: 50px;
  }
}
</style>
