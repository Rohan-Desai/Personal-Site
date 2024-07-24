<script setup>
import JobPage from '/src/components/JobGeneric.vue'

const cluesExperience = {
  title: 'Full Stack Developer',
  subtitle: 'University Researcher',
  company: 'Learning Clues',
  acronym: 'ontextual inkages ndergraduate ducation ystem',
  content: [
    'utilizes react.js, figma, openAI api, aws, node.js, python, javascript, docker',

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
  ]
}

const moralityExperience = {
  title: 'Full-Stack Developer',
  subtitle: 'University Researcher',
  company: 'Morality Game',
  content: [
    'Utilizes React.js, AWS, Node.js, Flask, Python, Javascript, Docker, PostgreSQL, HTML',
    'Collaborated with team to develop a web app that implements behavioral economics to study cooperation',
    'Developed documentation with Sphinx, enhancing understanding among team members to save over 20 hours per developer during onboarding and development',
    'Implemented Paypal Payouts and Checkout API to facilitate over $1000 of secure payments between researchers and participants',
    'Implemented UofM SONA API to grant credit, ensure anonymity, and recruit over 200 participants'
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
  ]
}

const g24Experience = {
  title: 'Front-End Developer',
  subtitle: 'Internship',
  company: 'Twenty-Four G',
  content: [
    'Utilized Vue.js, Javascript, HTML, AdobeXD, Swagger, Vault',
    'Developed a comprehensive AI training application for employees using specialized knowledge bases from scratch',
    'Completed training in Entrepreneurial Operating Systems (EOS) and Secure Software Development Life Cycle (SDLC)',
    'Mastered Vue.js ecosystem including Vue, Vue Pinia, Vue Router, and VueX',
    'Leveraged Agile methodologies focusing on sprint cycles, completing 6 major releases over 3 months',
    'Enhanced API integration and functionality by coordinating requirements and feedback with backend teams, aligning end-to-end system performance with client expectations, and reducing response times by 15%',
    'Collaborated directly with end clients to gather comprehensive service requirements and customized features for companies with over 1000 employees',
    'Implemented and managed unit testing to ensure robustness and reliability, saving over 100 hours of testing'
  ],
  tags: [
    'Vue.js',
    'Javascript',
    'HTML',
    'AdobeXD',
    'Swagger',
    'Vault',
    'Entrepreneurial Operating Systems (EOS)',
    'Vue Pinia',
    'Vue Router',
    'Secure Software Development Life Cycle (SDLC)',
    'VueX',
    'Agile Methodologies',
    'API Integration',
    'Unit Testing'
  ]
}
</script>

<template>
  <div class="job-container">
    <JobPage
      :title="cluesExperience.title"
      :company="cluesExperience.company"
      :subtitle="cluesExperience.subtitle"
      :content="cluesExperience.content"
      :tags="cluesExperience.tags"
      :acronym="cluesExperience.acronym"
    />
    <JobPage
      :title="moralityExperience.title"
      :company="moralityExperience.company"
      :subtitle="moralityExperience.subtitle"
      :content="moralityExperience.content"
      :tags="moralityExperience.tags"
      :acronym="moralityExperience.acronym"
    />
    <JobPage
      :title="g24Experience.title"
      :company="g24Experience.company"
      :subtitle="g24Experience.subtitle"
      :content="g24Experience.content"
      :tags="g24Experience.tags"
      :acronym="g24Experience.acronym"
    />
  </div>
</template>

<style>
/* You can add additional styles here if needed */
</style>
