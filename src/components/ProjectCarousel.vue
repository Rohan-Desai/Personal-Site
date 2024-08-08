<script setup>
import { onMounted, ref, onBeforeUnmount } from 'vue'
import { gsap } from 'gsap'
import { Draggable } from 'gsap/Draggable'
import projectData from '/src/components/project.json'
import SkillButton from '/src/components/SkillButton.vue'

const projects = ref([])

// eslint-disable-next-line no-undef
gsap.registerPlugin(Draggable)

const containerRef = ref(null)

const calculateMinX = () => {
  // const containerWidth = containerRef.value.offsetWidth
  const viewportWidth = window.innerWidth
  if (viewportWidth > 1100) {
    return -2500
  } else if (viewportWidth < 1100 && viewportWidth > 850) {
    return -1800
  } else if (viewportWidth < 850 && viewportWidth > 500) {
    return -1500
  } else if (viewportWidth < 500) {
    return -1650
  }
  return 0
}

const initializeDraggable = () => {
  const container = containerRef.value

  Draggable.create(container, {
    type: 'x',
    bounds: { minX: calculateMinX(), maxX: 0 },
    edgeResistance: 0.8,
    inertia: true
  })

  const scrollDuration = 30 // Duration for one complete scroll
  const tl = gsap.timeline({ repeat: -1 }) // Infinite repeat
  tl.to(container, {
    x: calculateMinX(),
    duration: scrollDuration,
    ease: 'none'
  }).to(container, {
    x: 0,
    duration: scrollDuration,
    ease: 'none'
  })
}

onMounted(() => {
  projects.value = projectData.projects
  initializeDraggable()
  window.addEventListener('resize', initializeDraggable)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', initializeDraggable)
})
</script>

<template>
  <div class="carousel-container">
    <div class="carousel-inner-container" ref="containerRef">
      <div class="carousel">
        <div
          v-for="project in projects"
          :key="project.id"
          class="carousel-item"
          :style="{ backgroundColor: project.color }"
        >
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>
          <div class="tags-wrapper">
            <div class="tags">
              <span v-for="tag in project.skills" :key="tag" class="tag">
                <SkillButton :skill="tag" />
              </span>
            </div>
          </div>
          <a v-if="project.links.github" :href="project.links.github" target="_blank">
            <i class="fab fa-github icon"></i>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.carousel-container {
  overflow: hidden; /* Ensure items are contained within the container */
}

.carousel-inner-container {
  display: flex;
  width: 100%;
}

.carousel {
  display: flex;
  cursor: grab;
}

.carousel:active {
  cursor: grabbing;
}

.carousel-item {
  min-width: 350px;
  height: 700px;
  margin: 0 1rem;
  padding: 1rem;
  /* background-color: #f4f4f4; */
  border-radius: 25px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.carousel-item h3 {
  margin-bottom: 0.5rem;
  font-size: 1.5rem;
  color: white;
  font-weight: 900;
  text-align: center;
  /* height: 25%; */
  justify-content: center;
  margin: auto;
}

.carousel-item p {
  margin-bottom: 1rem;
  font-size: 1rem;
  color: white;
  margin: auto;
}
.tags-wrapper {
  margin: auto;
}
.skill-button {
  padding: 7px 10px;
  margin: 6px;
  border-radius: 50px; /* Rounded corners */
  font-size: 0.7vw; /* Font size */
}
.carousel-item a {
  margin: auto;
}
.icon {
  font-size: 30px;
  color: white;
}
@media (min-width: 1800px) {
  .carousel-item {
    min-width: 450px;
    height: 1000px;
    margin: 0 1rem;
    padding: 1rem;
  }
  .carousel-item h3 {
    font-size: 2rem;
  }

  .carousel-item p {
    font-size: 1.2rem;
  }
  .icon {
    font-size: 50px;
    color: white;
  }
}
/* @media (max-width: 1800px) and (min-width: 1600px) {
} */
@media (max-width: 1100px) and (min-width: 850px) {
  .carousel-item {
    min-width: 250px;
    height: 450px;
    margin: 0 1rem;
    padding: 1rem;
  }
  .carousel-item h3 {
    font-size: 1rem;
  }

  .carousel-item p {
    font-size: 0.7rem;
  }
  .icon {
    font-size: 20px;
    color: white;
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .carousel-item {
    min-width: 200px;
    height: 320px;
    margin: 0 1rem;
    padding: 1rem;
  }
  .carousel-item h3 {
    font-size: 0.7rem;
  }

  .carousel-item p {
    font-size: 0.5rem;
  }
  .icon {
    font-size: 20px;
    color: white;
  }
  .skill-button {
    padding: 5px 7px;
    margin: 2px;
    font-size: 0.3rem; /* Font size */
  }
}
@media (max-width: 500px) {
  .carousel-item {
    min-width: 200px;
    height: 320px;
    margin: 0 1rem;
    padding: 1rem;
  }
  .carousel-item h3 {
    font-size: 0.7rem;
  }

  .carousel-item p {
    font-size: 0.5rem;
  }
  .icon {
    font-size: 20px;
    color: white;
  }
  .skill-button {
    padding: 5px 7px;
    margin: 2px;
    font-size: 0.3rem; /* Font size */
  }
}
</style>
