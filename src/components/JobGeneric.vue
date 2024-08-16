<script setup>
import { defineProps, onMounted } from 'vue'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

import SkillButton from '/src/components/SkillButton.vue'
import { gsap } from 'gsap'
gsap.registerPlugin(ScrollTrigger)

// Define props
const props = defineProps({
  title: {
    type: String,
    required: true
  },
  subtitle: {
    type: String,
    required: true
  },
  company: {
    type: String,
    required: true
  },
  content: {
    type: Array,
    required: true
  },
  tags: {
    type: Array,
    required: true
  },
  pageType: {
    type: String,
    required: true
  }
})

// Split the company name into an array of words
const companyWords = props.company.split(' ')
const rotatedTexts = ['ystem', 'ducation', 'ndergraduate', 'inkages', 'ontextual']

onMounted(() => {
  if (props.pageType === 'LC') {
    gsap.fromTo(
      '.rotated-text span',
      {
        opacity: 0,
        y: -20
      },
      {
        opacity: 1,
        y: 0,
        stagger: -0.5,
        duration: 1,
        ease: 'power2.out',
        repeat: -1, // Infinite repeat
        yoyo: true // Plays forward and then backward
      }
    )
  }
})
</script>

<template>
  <div class="job-page">
    <div class="header">
      <h1>{{ title }}</h1>
      <h3>{{ subtitle }}</h3>
    </div>
    <div class="main-content">
      <div class="company-name">
        <!-- Render each word with specific style -->
        <p>
          <span v-for="(word, index) in companyWords" :key="index" :class="word">{{ word }}</span>
        </p>
        <!-- <p><span class="Clues">Clues</span></p> -->
        <div class="rotated-text" v-if="pageType == 'LC'">
          <span v-for="(text, index) in rotatedTexts" :key="index">{{ text }}</span>
        </div>
      </div>
      <div class="divider"></div>
      <div class="job-content">
        <ul>
          <li v-for="item in content" :key="item">{{ item }}</li>
        </ul>
        <div class="tags-wrapper">
          <div class="tags">
            <span v-for="tag in tags" :key="tag" class="tag">
              <SkillButton :skill="tag" />
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.job-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  height: 100vh;
}

.header {
  text-align: center;
  font-family: 'Major Mono Display';
  color: white;
}

.header h1 {
  font-size: 5vw;
}

.header h3 {
  font-size: 2vw;
}

.main-content {
  display: flex;
  width: 100%;
  color: white;
  margin-top: 50px;
}

.company-name {
  flex: 1;
  font-family: 'Major Mono Display';
  font-size: 7vw;
  position: relative;
  top: 20px;
}

.company-name p {
  text-align: center;
  display: flex;
  align-content: flex-start;
  flex-wrap: wrap;
  justify-content: center;
}
.company-name p .Learning {
  color: #7b70f5;
}
.company-name p .Clues {
  color: #dd64fb;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}
.company-name p .Morality {
  color: #fc334b;
}
.company-name p .Game {
  color: #f57d39;
}
.company-name p .Twenty-Four {
  color: #ffef63;
}
.company-name p .G {
  color: #aa5df8;
}

.rotated-text {
  display: flex;
  flex-direction: column;
  margin-top: 0px;
  margin-right: 40px;
  transform: rotate(90deg);
}

.rotated-text span {
  font-size: 1.5vw;
  color: #dd64fb;
  margin-bottom: 2.8vw;
  margin-left: 14vh;
}
.divider {
  position: relative;
  width: 1px;
  background-color: #fff;
  height: 80%;
  top: 0px;
}

.job-content {
  flex: 1;
  padding-left: 20px;
  color: #fff;
  font-family: 'Major Mono Display';
  font-size: 1.3vw;
  position: relative;
  top: 10px;
  color: white;
}

.job-content ul li {
  margin-bottom: 20px;
}
.tags {
  margin-top: 50px;
  margin-bottom: 20px;
}

.tag {
  display: inline-block;
  margin-right: 5px;
  margin-bottom: 5px;
}
.company-word {
  margin-right: 5px;
  /* Add any additional styles for each word here */
}

@media (min-width: 2400px) {
  .job-content {
    padding-left: 50px;
  }
  .tag {
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .main-content {
    margin-top: 100px;
  }
  .company-name {
    font-size: 7vw;
    /* top: 100px; */
  }
  .job-content {
    padding-left: 50px;
    font-size: 0.9vw;
    /* top: 50px; */
    color: white;
  }
  .tags {
    margin-top: 100px;
    margin-bottom: 50px;
  }

  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 18vh;
  }
}
@media (max-width: 2400px) and (min-width: 1800px) {
  .job-content {
    padding-left: 50px;
  }
  .tag {
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .main-content {
    margin-top: 100px;
  }
  .company-name {
    font-size: 7vw;
    /* top: 100px; */
  }
  .job-content {
    padding-left: 50px;
    font-size: 0.8vw;
    /* top: 50px; */
    color: white;
  }
  .tags {
    margin-top: 50px;
    margin-bottom: 50px;
  }
  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 14vh;
  }
}
@media (max-width: 1800px) and (min-width: 1600px) {
  .job-content {
    padding-left: 50px;
  }
  .tag {
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .main-content {
    margin-top: 50px;
  }
  .company-name {
    font-size: 7vw;
    /* top: 100px; */
  }
  .job-content {
    padding-left: 50px;
    font-size: .8vw;
    /* top: 20px; */
    color: white;
  }
  .tags {
    margin-top: 50px;
    margin-bottom: 50px;
  }
  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 12vh;
  }
}
@media (max-width: 1600px) and (min-width: 1380px) {
  .job-content {
    padding-left: 10px;
  }
  .tag {
    margin-right: 10px;
    margin-bottom: 10px;
  }
  .main-content {
    margin-top: 50px;
  }
  .company-name {
    font-size: 7vw;
    /* top: 100px; */
  }
  .G{
    font-size: 6vw;
  }
  .Twenty-Four{
    font-size: 6vw;

  }
  .job-content {
    padding-left: 50px;
    font-size: .7vw;
    /* top: 20px; */
    color: white;
  }
  .tags {
    margin-top: 25px;
    margin-bottom: 25px;
  }
  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 14vh;
  }
}
@media (max-width: 1380px) and (min-width: 850px) {
  .job-content {
    padding-left: 10px;
  }
  .tag {
    margin-right: 10px;
    margin-bottom: 10px;
  }
  .main-content {
    margin-top: 20px;
  }
  .company-name {
    font-size: 7vw;
    /* top: 100px; */
  }
  .job-content {
    padding-left: 20px;
    font-size: .6vw;
    /* top: 20px; */
    color: white;
  }
  .tags {
    margin-top: 25px;
    margin-bottom: 25px;
  }
  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 11vh;
  }
}
@media (max-width: 850px) and (min-width: 500px) {
  .job-content {
    padding-left: 10px;
  }
  .job-content ul {
    padding-left: 10px;
  }
  .tag {
    margin-right: 5px;
    margin-bottom: 5px;
  }
  .main-content {
    margin-top: 20px;
  }
  .company-name {
    font-size: 7vw;
    top: 150px;
  }
  .job-content {
    padding-left: 20px;
    font-size: 1.8vw;
    top: 20px;
    color: white;
  }
  .tags {
    margin-top: 5px;
    margin-bottom: 5px;
  }
  .rotated-text {
    margin-right: 3vw;
  }
  .rotated-text span {
    margin-left: 6vh;
  }
}
@media (max-width: 500px) {
  .job-content {
    padding-left: 10px;
  }
  .job-content ul {
    padding-left: 10px;
  }
  .tag {
    margin-right: 2px;
    margin-bottom: 2px;
  }
  .main-content {
    margin-top: 20px;
  }
  .company-name {
    font-size: 7vw;
    top: 200px;
    margin-right: 20px;
  }
  .job-content {
    padding-left: 20px;
    font-size: 2vw;
    top: 20px;
    color: white;
  }
  .tags {
    margin-top: 5px;
    margin-bottom: 5px;
  }
  .rotated-text {
    margin-right: 1vw;
  }
  .rotated-text span {
    margin-left: 3vh;
  }
}
</style>
