<script setup>
import ProjectCarousel from '/src/components/ProjectCarousel.vue'
</script>

<template>
  <div class="project-page-container">
    <div class="proj">
      <div class="title">
        <h1>Projects</h1>
      </div>
      <div class="project-content">
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
.project-content {
  display: flex;
  align-items: baseline;
  justify-content: flex-start;
}
.side-description {
  height: 50%;
  width: 40%;
  text-align: center;
  justify-content: center;
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
  /* /* bottom: 450px; */
  left: 5%;
}
@media (min-width: 1100px) {
  .proj {
    padding: 25px;
  }
  .title {
    font-size: 2.5rem;
  }
  .side-description .header {
    font-size: 2rem;
  }
  .side-description .description {
    font-size: 1.2rem;
  }
}
@media (max-width: 1100px) and (min-width: 850px) {
  .proj {
    padding: 25px;
  }
  .title {
    font-size: 2rem;
    margin-bottom: 5vh;
  }
  .side-description .header {
    font-size: 1.4rem;
  }
  .side-description .description {
    font-size: 0.9rem;
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .proj {
    padding: 15px;
  }
  .title {
    font-size: 1.5rem;
    margin-bottom: 5vh;
  }
  .side-description {
    width: 80%;
    margin: 0px auto 50px auto;
  }
  .side-description .header {
    font-size: 1.2rem;
  }
  .side-description .description {
    font-size: 0.8rem;
  }
  .project-content {
    display: flex;
    flex-direction: column;
  }
  .carousel-containers {
    width: 90%;
    margin: auto;
    left: 0;
    height: 100%;
  }
}
@media (max-width: 500px) {
  .proj {
    padding: 15px;
  }
  .title {
    font-size: 1.5rem;
    margin-bottom: 5vh;
  }
  .side-description {
    width: 80%;
    margin: 0px auto 50px auto;
  }
  .side-description .header {
    font-size: 1.2rem;
  }
  .side-description .description {
    font-size: 0.8rem;
  }
  .project-content {
    display: flex;
    flex-direction: column;
  }
  .carousel-containers {
    width: 90%;
    margin: auto;
    left: 0;
    height: 100%;
  }
}
</style>
