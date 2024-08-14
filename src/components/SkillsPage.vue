<script setup>
import { onMounted, ref, nextTick } from 'vue'
import { gsap } from 'gsap'
import SkillsData from '/src/components/Skills.json'
import SkillButton from '/src/components/SkillButton.vue'

const techSkills = ref([])
const softSkills = ref([])
const miscSkills = ref([])

const colors = ['#f3f3f3', '#ededed', '#fefeff', '#f3f3f3'] // Array of colors to use

const animateDiagonalWave = (buttons, numRows, numCols) => {
  const tl = gsap.timeline({ repeat: -1, repeatDelay: 2 }) // Repeat the animation with a delay of 2 seconds

  buttons.forEach((button, index) => {
    const row = Math.floor(index / numCols)
    const col = (index % numCols) + 1
    const diagonalIndex = row + col

    const delay = diagonalIndex * 0.2 // Adjust the multiplier to control wave speed

    const colorIndex = Math.floor(index / numRows) % colors.length // Determine the color based on the index
    const selectedColor = colors[colorIndex]

    tl.fromTo(
      button,
      { scale: 1, backgroundColor: '#e0e0e0' }, // Initial color (light gray)
      {
        scale: 1.2,
        backgroundColor: selectedColor, // Use the selected color
        duration: 0.4,
        ease: 'power1.inOut',
        yoyo: true,
        repeat: 1
      },
      delay
    )
  })
}

onMounted(async () => {
  techSkills.value = SkillsData.SkillsPage[0].skills
  softSkills.value = SkillsData.SkillsPage[1].skills
  miscSkills.value = SkillsData.SkillsPage[2].skills

  await nextTick() // Wait for DOM to update

  // Get skill buttons from each section
  const techButtons = [...document.querySelectorAll('.ttags')]
  const softButtons = [...document.querySelectorAll('.stags')]
  const miscButtons = [...document.querySelectorAll('.mtags')]

  // Animate buttons in a diagonal wave pattern for each section
  const numCols = 4 // Number of buttons per row

  // Calculate rows for each section
  const numRowsTech = Math.ceil(techButtons.length / numCols)
  const numRowsSoft = Math.ceil(softButtons.length / numCols)
  const numRowsMisc = Math.ceil(miscButtons.length / numCols)

  animateDiagonalWave(techButtons, numRowsTech, numCols)
  animateDiagonalWave(softButtons, numRowsSoft, numCols)
  animateDiagonalWave(miscButtons, numRowsMisc, numCols)
})
</script>

<template>
  <div class="skills-page-container">
    <div class="skills-page-title"><h1>Skills</h1></div>
    <div class="skills-content">
      <div class="left-section">
        <div class="technical-skills">
          <div class="skills-section-title"><h2>Technical</h2></div>
          <div class="skills-section-content gradient-background">
            <span v-for="tag in techSkills" :key="tag" class="tech-tag">
              <SkillButton :skill="tag" class="ttags" />
            </span>
          </div>
        </div>
      </div>
      <div class="vert-line"></div>
      <div class="right-section">
        <div class="soft-skills">
          <div class="skills-section-title"><h2>Soft</h2></div>
          <div class="skills-section-content gradient-background">
            <span v-for="tag in softSkills" :key="tag" class="soft-tag">
              <SkillButton :skill="tag" class="stags" />
            </span>
          </div>
        </div>
        <div class="horizontal-line"></div>
        <div class="miscellaneous-skills">
          <div class="skills-section-title"><h2>Miscellaneous</h2></div>
          <div class="skills-section-content gradient-background">
            <span v-for="tag in miscSkills" :key="tag" class="misc-tag">
              <SkillButton :skill="tag" class="mtags" />
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.skills-page-container {
  height: 100vh;
  position: relative;
  color: white;
  font-family: 'Major Mono Display', monospace;
  font-weight: 400;
  padding: 0px;
}

.skills-page-title {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 2vh;
  letter-spacing: 0.1em;
}

.skills-content {
  display: flex;
  flex-direction: row;
  width: 100%;
}

.left-section {
  width: 50%;
}

.technical-skills {
  height: 100%;
  width: 45vw;
  padding: 30px;
}

.right-section {
  display: flex;
  flex-direction: column;
  width: 50%;
  padding: 30px;
}

.soft-skills {
  height: 45%;
  width: 45vw;
}

.miscellaneous-skills {
  height: 45%;
  width: 45vw;
}

.skills-section-title {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 3vh;
  letter-spacing: 0.1em;
}

.vert-line {
  width: 2px;
  background-color: white;
  height: 80vh;
  position: relative;
  top: 50px;
}

.horizontal-line {
  height: 2px;
  background-color: white;
  width: 80vh;
  position: relative;
  margin: 30px;
}

.skills-section-content {
  display: flex;
  flex-wrap: wrap; /* Allows for responsive wrapping of buttons */
}

.skill-button {
  padding: 10px 10px;
  margin: 5px;
  font-size: 1.1rem; /* Font size */
  background-clip: border-box;
}
.tech-tag,
.soft-tag,
.misc-tag {
  transition: transform 0.3s ease;
}

@media (min-width: 2400px) {
  .skills-page-title {
    font-size: 5rem;
  }
  .skills-section-title {
    font-size: 3rem;
  }
  .skill-button {
    padding: 15px 15px;
    margin: 8px;
    font-size: 2rem; /* Font size */
  }
}
@media (max-width: 2400px) and (min-width: 1800px) {
  .skills-page-title {
    font-size: 4rem;
  }
  .skills-section-title {
    font-size: 3rem;
  }
  .skill-button {
    padding: 15px 15px;
    margin: 8px;
    font-size: 1.4rem; /* Font size */
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
  .skill-button {
    padding: 10px 10px;
    margin: 5px;
    font-size: 1rem; /* Font size */
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .skill-button {
    padding: 10px 10px;
    margin: 4px;
    font-size: 0.8rem; /* Font size */
  }
}
@media (max-width: 1380px) and (min-width: 850px) {
  .skills-page-title {
    font-size: 2rem;
  }
  .skills-section-title {
    font-size: 1.3rem;
  }
  .skill-button {
    padding: 8px 8px;
    margin: 3px;
    font-size: 0.7rem; /* Font size */
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .skills-content {
    flex-direction: column;
  }
  .skills-page-title {
    font-size: 1.3rem;
    margin-bottom: 0;
  }
  .skills-section-title {
    font-size: 1rem;
  }
  .skill-button {
    padding: 6px 6px;
    margin: 2px;
    font-size: 0.6rem; /* Font size */
  }
  .vert-line {
    width: 0px;
  }
  .left-section {
    width: 100%;
  }

  .technical-skills {
    width: 100vw;
    padding: 30px;
  }
  .skills-content {
    height: 50%;
  }
  .right-section {
    width: 100%;
    padding-top: 0;
  }

  .soft-skills {
    width: 95vw;
    /* padding: 30px; */
  }
  .miscellaneous-skills {
    width: 95vw;
    /* padding: 30px; */
  }
  .horizontal-line {
    height: 0px;
    margin: 20px;
  }
  .vert-line {
    display: none;
  }
}
@media (max-width: 500px) {
  .skills-content {
    flex-direction: column;
  }
  .skills-page-title {
    font-size: 1.3rem;
    margin-bottom: 0;
  }
  .skills-section-title {
    font-size: 1rem;
  }
  .skill-button {
    padding: 5px 5px;
    margin: 2px;
    font-size: 0.4rem; /* Font size */
  }
  .vert-line {
    width: 0px;
  }
  .left-section {
    width: 100%;
  }

  .technical-skills {
    width: 100vw;
    padding: 30px;
  }
  .skills-content {
    height: 50%;
  }
  .right-section {
    width: 100%;
    padding-top: 0;
  }

  .soft-skills {
    width: 90vw;
    /* padding: 30px; */
  }
  .miscellaneous-skills {
    width: 90vw;
    /* padding: 30px; */
  }
  .horizontal-line {
    height: 0px;
    margin: 20px;
  }
  .vert-line {
    display: none;
  }
}
</style>
