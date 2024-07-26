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

onMounted(() => {
  gsap.set(section1.value, { autoAlpha: 0 })
  gsap.set(section2.value, { autoAlpha: 0 })
  gsap.set(section3.value, { autoAlpha: 0 })

  ScrollTrigger.create({
    trigger: '.job-container',
    start: 'top top',
    end: 'bottom bottom',
    scrub: true,
    pin: true,
    id: 'myScrollTrigger2',
    onUpdate: (self) => {
      const progress = self.progress
      if (progress < 0.33) {
        gsap.to(section1.value, { autoAlpha: 1 })
        gsap.to(section2.value, { autoAlpha: 0 })
        gsap.to(section3.value, { autoAlpha: 0 })
      } else if (progress < 0.66) {
        gsap.to(section1.value, { autoAlpha: 0 })
        gsap.to(section2.value, { autoAlpha: 1 })
        gsap.to(section3.value, { autoAlpha: 0 })
      } else if (progress < 1) {
        gsap.to(section1.value, { autoAlpha: 0 })
        gsap.to(section2.value, { autoAlpha: 0 })
        gsap.to(section3.value, { autoAlpha: 1 })
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
  height: 200vh;
  position: relative;
}
.scroll-container {
  position: relative;
}

.job-page {
  height: 100vh; /* Each section takes full viewport height */
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
  /* opacity: 0; Set initial opacity to 0 for all sections */
}
</style>
