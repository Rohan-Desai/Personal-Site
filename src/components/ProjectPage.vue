<script setup>
import ProjectCarousel from '/src/components/ProjectCarousel.vue'
</script>

<template>
  <div class="project-page-container">
    <div class="proj">
      <div class="title">
        <h1>Projects</h1>
      </div>
      <div class="content">
        <div class="side-description">
          <div class="header">
            <h2>Intersecting Interests</h2>
          </div>
          <div class="description">
            <h3>
              Explore the unique convergence of my personal passions and professional expertise.
              This collection of projects highlights how I blend diverse interests like music,
              culture, and wellness with cutting-edge technology to create innovative solutions.
            </h3>
          </div>
        </div>
        <div class="carousel-containers">
          <ProjectCarousel />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.project-page-container {
  color: white;
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  height: 100vh;
}
.proj {
  height: 100vh;
  width: 100%;
  padding: 50px;
}
.title {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 10vh;
  letter-spacing: 0.1em;
}
.content {
  display: flex;
}
.side-description {
  height: 50%;
  width: 40%;
  text-align: center;
}
.side-description .header {
  font-size: 3rem;
  color: #7d8aff;
}
.side-description .description {
  font-size: 1.3rem;
}
.carousel-containers {
  position: relative;
  height: 80%;
  width: 55%;
  /* bottom: 450px;
  left: 45%; */
}
@media (min-width: 1800px) {
  .proj {
    padding: 100px;
  }
  .title {
    font-size: 5rem;
  }
  .side-description .header {
    font-size: 3rem;
  }
  .side-description .description {
    font-size: 2rem;
  }
  .carousel-containers {
    position: relative;
    height: 80%;
    width: 55%;
    bottom: 850px;
    left: 45%;
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
}
@media (max-width: 1380px) and (min-width: 850px) {
}
@media (max-width: 850px) and (min-width: 500px) {
}
@media (max-width: 500px) {
}
</style>
