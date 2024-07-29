<script setup>
import JobPage from '/src/components/JobGeneric.vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { onMounted, onBeforeUnmount } from 'vue'
import { ref } from 'vue'

gsap.registerPlugin(ScrollTrigger)

const cluesExperience = {
  title: 'Full Stack Developer',
  subtitle: 'University Researcher',
  company: 'Learning Clues',
  acronym: 'Contextual Linkages Undergraduate Education System',
  content: [
    'utilizes react.js, figma, openai api, aws, node.js, python, javascript, docker',
    'chatbot designed to assist students by scraping content from course pages to provide accurate, contextually relevant answers.',
    "developed a 'suggested queries' feature providing potential questions to ask the model, improving engagement and usability.",
    'conducted security testing using dynamic and static application security testing, finding and fixing over 30+ vulnerabilities'
  ],
  tags: [
    'React.js',
    'Figma',
    'OpenAI API',
    'AWS',
    'Node.js',
    'Python',
    'Javascript',
    'Docker',
    'TypeScript',
    'REST APIs',
    'Web Development',
    'Dynamic Application Security Testing',
    'Static Application Security Testing'
  ],
  pageType: 'LC'
}

const moralityExperience = {
  title: 'Full-Stack Developer',
  subtitle: 'University Researcher',
  company: 'Morality Game',
  content: [
    'utilizes react.js, aws, node.js, flask, python, javascript, docker, postgresql, html',
    'collaborated with team to develop a web app that implements behavioral economics to study cooperation',
    'developed documentation with sphinx, enhancing understanding among team members to save over 20 hours per developer during onboarding and development',
    'implemented paypal payouts and checkout api to facilitate over $1000 of secure payments between researchers and participants',
    'implemented uofm sona api to grant credit, ensure anonymity, and recruit over 200 participants'
  ],
  tags: [
    'React.js',
    'AWS',
    'Node.js',
    'Flask',
    'Python',
    'Javascript',
    'Docker',
    'PostgreSQL',
    'Behavioral Economics',
    'Sphinx',
    'Paypal'
  ],
  pageType: 'MG'
}

const g24Experience = {
  title: 'Front-End Developer',
  subtitle: 'Internship',
  company: 'Twenty-Four G',
  content: [
    'developed a comprehensive ai training application for employees using specialized knowledge bases from scratch',
    'completed training in entrepreneurial uperating systems (eos) and secure software development life cycle (sdlc)',
    'enhanced api integration and functionality by coordinating requirements and feedback with backend teams, aligning end-to-end system performance with client expectations, and reducing response times by 15%',
    'implemented and managed unit testing to ensure robustness and reliability, saving over 100 hours of testing'
  ],
  tags: [
    'Vue.js',
    'Javascript',
    'HTML',
    'AdobeXD',
    'Swagger',
    'Vault',
    'Entrepreneurial Operating Systems',
    'Vue Pinia/Router/X',
    'Unit Testing',
    'Software Development Life Cycle',
    'Agile Methodologies',
    'API Integration'
  ],
  pageType: 'TFG'
}

const section1 = ref(null)
const section2 = ref(null)
const section3 = ref(null)
const isSection1Trans = ref(true)
const isSection2Trans = ref(false)
const isSection3Trans = ref(false)

const slideBg = ref(null)

const animateSlide = (targetSection) => {
  gsap
    .timeline()
    .to(slideBg.value, { xPercent: 0, duration: 0.5, ease: 'power2.inOut', borderRadius: 0 })
    .set(
      [section1.value, section2.value, section3.value].filter((el) => el !== targetSection),
      { autoAlpha: 0 }
    )
    .set(targetSection, { autoAlpha: 1 }, '<')
    .to(slideBg.value, {
      xPercent: -100,
      duration: 0.5,
      delay: 0.5,
      ease: 'power2.inOut',
      borderRadius: '50%'
    })
}

onMounted(() => {
  gsap.set(section1.value, { autoAlpha: 1 })
  gsap.set(section2.value, { autoAlpha: 0 })
  gsap.set(section3.value, { autoAlpha: 0 })
  gsap.set(slideBg.value, { xPercent: -100 })

  ScrollTrigger.create({
    trigger: '.job-container',
    start: 'top top',
    end: 'bottom bottom',
    scrub: true,
    pin: true,
    id: 'myScrollTrigger2',
    onUpdate: (self) => {
      //On Enter
      if (self.progress < 0.33 && !isSection1Trans.value) {
        animateSlide(section1.value)
        isSection1Trans.value = true
        isSection2Trans.value = false
        isSection3Trans.value = false
      } else if (self.progress > 0.33 && self.progress < 0.66 && !isSection2Trans.value) {
        animateSlide(section2.value)
        isSection2Trans.value = true
        isSection1Trans.value = false
        isSection3Trans.value = false
      } else if (self.progress > 0.66 && self.progress < 1 && !isSection3Trans.value) {
        animateSlide(section3.value)
        isSection3Trans.value = true
        isSection1Trans.value = false
        isSection2Trans.value = false
      }
    }
  })
  ScrollTrigger.refresh()
})

onBeforeUnmount(() => {
  ScrollTrigger.getAll().forEach((trigger) => trigger.kill())
})
</script>

<template>
  <div class="job-container">
    <div class="slide-bg" ref="slideBg"></div>
    <div>
      <div class="job-page" ref="section1">
        <JobPage
          :title="cluesExperience.title"
          :company="cluesExperience.company"
          :subtitle="cluesExperience.subtitle"
          :content="cluesExperience.content"
          :tags="cluesExperience.tags"
          :acronym="cluesExperience.acronym"
          :pageType="cluesExperience.pageType"
        />
      </div>
    </div>
    <div>
      <div class="job-page" ref="section2">
        <JobPage
          :title="moralityExperience.title"
          :company="moralityExperience.company"
          :subtitle="moralityExperience.subtitle"
          :content="moralityExperience.content"
          :tags="moralityExperience.tags"
          :pageType="moralityExperience.pageType"
        />
      </div>
    </div>
    <div>
      <div class="job-page" ref="section3">
        <JobPage
          :title="g24Experience.title"
          :company="g24Experience.company"
          :subtitle="g24Experience.subtitle"
          :content="g24Experience.content"
          :tags="g24Experience.tags"
          :pageType="g24Experience.pageType"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.job-container {
  height: 200vh; /* Updated to reflect the correct height */
  position: relative;
}

.slide-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #000; /* Change to desired monochrome background color */
  z-index: 1;
  border-radius: 50%;

  /* display: none; */
}

.job-page {
  height: 100vh; /* Each section takes full viewport height */
  position: absolute;
  width: 100%;
  z-index: 0;
  top: 0;
  left: 0;
}
</style>
