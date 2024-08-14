<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import CourseCard from '/src/components/CourseCard.vue'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  gsap.to('#page2', {
    yPercent: -100,
    ease: 'none',
    scrollTrigger: {
      trigger: '.education',
      start: 'top top',
      end: 'bottom top',
      scrub: true,
      pin: true
    }
  })
})
</script>

<template>
  <div class="education">
    <div class="page" id="page1">
      <h1 class="main-title">Education</h1>
      <div class="college">
        <div class="school">
          <div class="icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 192.756 192.756">
              <g fill-rule="evenodd" clip-rule="evenodd">
                <path
                  fill="#293b5a"
                  d="M16.257 38.406v34.273h12.428v47.132H16.257v34.541h62.015v-34.541H65.446V92.702l30.931 41.189 30.932-41.187v27.107h-12.827v34.539h62.016v-34.539H164.07V72.679h12.428V38.406h-48.646L96.377 82.133 64.903 38.406H16.257z"
                />
                <path
                  fill="#f2ca30"
                  d="M96.377 86.252l32.709-45.44h45.006v29.461h-12.428v51.944h12.428v29.726h-57.203v-29.726h12.826V85.492l-33.338 44.391L63.04 85.492v36.725h12.827v29.728H18.663l.001-29.728h12.427V70.273H18.664V40.812H63.67l32.707 45.44z"
                />
              </g>
            </svg>
          </div>
          <div class="heading">
            <h3 class="title">university of michigan - ann arbor</h3>
            <h3 class="major">B.S computer science</h3>
            <h3 class="minor">B.S cognitive science</h3>
          </div>
        </div>
        <div class="vert-line"></div>
        <div class="information">
          <h3 class="gpa">gpa: 3.6/4.00</h3>
          <h3 class="activities">
            activities: m3 lab (mind, machines, and mathematics), mdp (multi-disciplinary design
            program), sigma chi fraternity, michigan data science team, michigan cognitive science
            society, algorithmic trading club
          </h3>
          <h3 class="awards">
            awards & honors: deans list, william j. branstorm prize, university honors
          </h3>
        </div>
      </div>
      <div class="high-school">
        <div class="schools">
          <div class="school">
            <div class="icon">
              <img
                src="/Users/rohandesai/Desktop/Personal Site Development/Personal Site/src/components/icons/Stevenson (1).png"
                alt="Stevenson High School Logo"
              />
            </div>
            <div class="heading">
              <h3 class="title">adlai e. stevenson high school</h3>
            </div>
          </div>
          <div class="school">
            <div class="icon">
              <img
                src="/Users/rohandesai/Desktop/Personal Site Development/Personal Site/src/components/icons/UCMST.png"
                alt="Utica Center for Math, Science, and Technology Logo"
              />
            </div>
            <div class="heading">
              <h3 class="title">utica center for math, science, and technology</h3>
            </div>
          </div>
        </div>
        <div class="vert-line"></div>
        <div class="information">
          <h3 class="gpa">gpa: 4.23/4.00</h3>
          <h3 class="activities">
            activities: coding club founder, ucs jazba (dance team) captain, ucs iasa president,
            varsity tennis captain, quizbowl captain
          </h3>
          <h3 class="awards">
            awards & honors: valedictorian, ap scholar with distinction, american math competition
            district high score
          </h3>
        </div>
      </div>
    </div>
    <div class="page" id="page2">
      <h1 class="main-title-course">Courses</h1>
      <CourseCard />
    </div>
  </div>
</template>

<style scoped>
.education {
  background-color: #2d4d76;
  color: white;
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  height: 100vh;
}
.page {
  height: 100vh;
  width: 100%;
  padding: 50px;
}
#page1 {
  position: relative;
  top: 0;
  left: 0;
  z-index: 1;
}
#page2 {
  background-color: #2d4d76;
  position: relative;
  top: 0;
  left: 0;
  z-index: 1;
}
.main-title {
  font-size: 4rem;
  text-align: center;
  margin-bottom: 10vh;
  letter-spacing: 0.1em;
}
.main-title-course {
  font-size: 4rem;
  text-align: center;
  margin-bottom: 3vh;
  letter-spacing: 0.1em;
}
.college,
.high-school {
  align-items: center; /* Center items vertically */
  height: 30vh;
  margin-top: 5vh;
}
.schools {
  position: relative;
  top: 10vh;
}
.high-school {
  position: relative;
  bottom: 20vh;
}
.school {
  display: flex;
  align-items: center;
  width: 45vw;
  margin-top: 10vh;
}

.icon img {
  margin-right: 1vw;
  width: 125px;
  height: 125px;
}
.icon svg {
  margin-right: 1vw;
  width: 125px;
  height: 125px;
}

.title,
.major,
.minor {
  margin: 0;
  font-size: 1.5rem;
}

.vert-line {
  width: 2px;
  background-color: white;
  height: 27vh;
  position: relative;
  bottom: 16vh;
  left: 46.5vw;
}

.information {
  position: relative;
  bottom: 43vh;
  left: 50vw;
  width: 45vw;
}

.gpa,
.activities,
.awards {
  margin: 0.5rem 0;
  line-height: 1.5;
}

@media (min-width: 1800px) {
  .main-title,
  .main-title-course {
    font-size: 6rem;
  }
  .title,
  .major,
  .minor {
    font-size: 2.5rem;
  }
  .information {
    font-size: 1.6rem;
  }
  .icon img {
    margin-right: 1vw;
    width: 200px;
    height: 200px;
  }
  .icon svg {
    margin-right: 1vw;
    width: 200px;
    height: 200px;
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
  .main-title,
  .main-title-course {
    font-size: 6rem;
  }
  .title,
  .major,
  .minor {
    font-size: 1.8rem;
  }
  .information {
    font-size: 1rem;
  }
  .icon {
    margin-right: 2vw;
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .main-title,
  .main-title-course {
    font-size: 4rem;
  }
  .title,
  .major,
  .minor {
    font-size: 1.6rem;
  }
  .information {
    font-size: 0.9rem;
  }
  .icon {
    margin-right: 2vw;
  }
}
@media (max-width: 1380px) and (min-width: 850px) {
  .main-title,
  .main-title-course {
    font-size: 4rem;
  }
  .title,
  .major,
  .minor {
    font-size: 1.2rem;
  }
  .information {
    font-size: 0.7rem;
  }
  .school {
    margin-top: 5vh;
  }
  .icon img {
    margin-right: 1vw;
    width: 80px;
    height: 80px;
  }
  .icon svg {
    margin-right: 1vw;
    width: 80px;
    height: 80px;
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .page {
    padding: 20px;
  }
  .main-title,
  .main-title-course {
    font-size: 3rem;
    margin-bottom: 5vh;
  }
  .title,
  .major,
  .minor {
    font-size: 0.8rem;
  }
  .information {
    font-size: 0.6rem;
  }
  .icon img {
    margin-right: 1vw;
    width: 80px;
    height: 80px;
  }
  .icon svg {
    margin-right: 1vw;
    width: 80px;
    height: 80px;
  }
  .school {
    margin-top: 0vh;
  }
  .information {
    width: 40vw;
  }
  .college {
    margin-top: 15vh;
  }
  .high-school {
    margin-top: 15vh;
  }
}
@media (max-width: 500px) {
  .page {
    padding: 25px;
  }
  .main-title,
  .main-title-course {
    font-size: 2rem;
  }
  .title,
  .major,
  .minor {
    font-size: 0.7rem;
  }
  .information {
    font-size: 0.5rem;
  }
  .icon img {
    margin-right: 2vw;
    width: 50px;
    height: 50px;
  }
  .icon svg {
    margin-right: 2vw;
    width: 50px;
    height: 50px;
  }
  .information {
    width: 35vw;
  }
  .college {
    margin-top: 15vh;
  }
  .high-school {
    margin-top: 15vh;
  }
}
</style>
