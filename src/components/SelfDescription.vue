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
          end: '+=' + window.innerWidth, // Adjust this value based on the length of your scroll
          scrub: true
        }
      })
    })
    const arrowAnimations = [
      { selector: '.arrow.rightdown', x: 400, y: 400 },
      { selector: '.arrow.leftdown', x: -400, y: 400 },
      { selector: '.arrow.rightup', x: 400, y: -400 },
      { selector: '.arrow.leftup', x: -400, y: -400 }
    ]

    arrowAnimations.forEach((arrow) => {
      gsap.fromTo(
        arrow.selector,
        { x: 0, y: 0 },
        {
          x: arrow.x,
          y: arrow.y,
          scrollTrigger: {
            trigger: '.wrapper',
            start: 'top top',
            end: '+=' + window.innerWidth * 1.2,
            scrub: true
          }
        }
      )
    })
    const lines = gsap.utils.toArray('.line svg')
    gsap.fromTo(
      lines,
      { width: 0 },
      {
        width: (i, target) => target.getAttribute('width'),
        scrollTrigger: {
          trigger: '.wrapper',
          start: 'top bottom',
          end: '+=' + window.innerWidth * 2.5,
          scrub: true
        },
        stagger: 0.2 // Adjust the stagger value as needed
      }
    )
    // Adding fall down animation for the "unknown" box
    gsap.fromTo(
      '.pinkbox',
      { y: -600, rotation: 0 },
      {
        y: 1500,
        rotation: 20,
        ease: 'power1.in',
        scrollTrigger: {
          trigger: '.wrapper',
          start: 'top center',
          end: '+=' + window.innerWidth * 6.7,
          scrub: true,
          onUpdate: (self) => {
            if (self.progress > 0.5) {
              gsap.to('.pinkbox', {
                ease: 'power1.out',
                overwrite: 'auto',
                scrollTrigger: {
                  trigger: '.wrapper',
                  start: 'top center',
                  end: '+=' + window.innerWidth * 7,
                  scrub: true,
                  immediateRender: false
                }
              })
            }
          }
        }
      }
    )
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
        <div class="arrow rightdown">
          <svg
            width="259"
            height="280"
            viewBox="0 0 259 280"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M251.818 279.997C254.578 280.097 256.896 277.941 256.997 275.182L258.63 230.211C258.731 227.452 256.575 225.133 253.815 225.033C251.056 224.933 248.737 227.089 248.637 229.848L247.185 269.822L207.211 268.37C204.452 268.269 202.133 270.425 202.033 273.185C201.933 275.944 204.089 278.263 206.848 278.363L251.818 279.997ZM-3.66156 7.40485L248.338 278.405L255.662 271.595L3.66156 0.595154L-3.66156 7.40485Z"
              fill="#FF6C6C"
            />
          </svg>
        </div>
        <div class="arrow leftdown">
          <svg
            width="259"
            height="280"
            viewBox="0 0 259 280"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M251.818 279.997C254.578 280.097 256.896 277.941 256.997 275.182L258.63 230.211C258.731 227.452 256.575 225.133 253.815 225.033C251.056 224.933 248.737 227.089 248.637 229.848L247.185 269.822L207.211 268.37C204.452 268.269 202.133 270.425 202.033 273.185C201.933 275.944 204.089 278.263 206.848 278.363L251.818 279.997ZM-3.66156 7.40485L248.338 278.405L255.662 271.595L3.66156 0.595154L-3.66156 7.40485Z"
              fill="#FF6C6C"
            />
          </svg>
        </div>
        <h1>carving <span class="boxed redbox">my own</span> path</h1>
        <div class="arrow rightup">
          <svg
            width="259"
            height="280"
            viewBox="0 0 259 280"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M251.818 279.997C254.578 280.097 256.896 277.941 256.997 275.182L258.63 230.211C258.731 227.452 256.575 225.133 253.815 225.033C251.056 224.933 248.737 227.089 248.637 229.848L247.185 269.822L207.211 268.37C204.452 268.269 202.133 270.425 202.033 273.185C201.933 275.944 204.089 278.263 206.848 278.363L251.818 279.997ZM-3.66156 7.40485L248.338 278.405L255.662 271.595L3.66156 0.595154L-3.66156 7.40485Z"
              fill="#FF6C6C"
            />
          </svg>
        </div>
        <div class="arrow leftup">
          <svg
            width="259"
            height="280"
            viewBox="0 0 259 280"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M251.818 279.997C254.578 280.097 256.896 277.941 256.997 275.182L258.63 230.211C258.731 227.452 256.575 225.133 253.815 225.033C251.056 224.933 248.737 227.089 248.637 229.848L247.185 269.822L207.211 268.37C204.452 268.269 202.133 270.425 202.033 273.185C201.933 275.944 204.089 278.263 206.848 278.363L251.818 279.997ZM-3.66156 7.40485L248.338 278.405L255.662 271.595L3.66156 0.595154L-3.66156 7.40485Z"
              fill="#FF6C6C"
            />
          </svg>
        </div>
      </div>
      <div id="panel3" class="panel center">
        <div class="line-container">
          <div class="line firstline">
            <svg width="100" height="25"></svg>
          </div>
          <div class="line secondline">
            <svg width="0" height="25"></svg>
          </div>
          <div class="line thirdline">
            <svg width="00" height="25"></svg>
          </div>
          <div class="line fourthline">
            <svg width="0" height="25"></svg>
          </div>
        </div>
        <h1><span class="boxed orangebox">pushing</span> the status quo</h1>
        <div class="line-container">
          <div class="line firstline">
            <svg
              width="100"
              height="25"
              viewBox="0 0 390 25"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <line y1="12.5" x2="389.021" y2="12.5" stroke="#FFAE63" stroke-width="25" />
            </svg>
          </div>
          <div class="line secondline">
            <svg
              width="200"
              height="25"
              viewBox="0 0 390 25"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <line y1="12.5" x2="389.021" y2="12.5" stroke="#FFAE63" stroke-width="25" />
            </svg>
          </div>
          <div class="line thirdline">
            <svg
              width="300"
              height="25"
              viewBox="0 0 390 25"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <line y1="12.5" x2="389.021" y2="12.5" stroke="#FFAE63" stroke-width="25" />
            </svg>
          </div>
          <div class="line fourthline">
            <svg
              width="400"
              height="25"
              viewBox="0 0 390 25"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <line y1="12.5" x2="389.021" y2="12.5" stroke="#FFAE63" stroke-width="25" />
            </svg>
          </div>
        </div>
      </div>
      <div id="panel4" class="panel center">
        <div class="oval topoval">
          <svg
            width="927"
            height="201"
            viewBox="0 0 927 201"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g filter="url(#filter0_d_21_23)">
              <ellipse cx="463.5" cy="96.5" rx="449.5" ry="86.5" fill="#FF63D3" />
            </g>
            <defs>
              <filter
                id="filter0_d_21_23"
                x="0"
                y="0"
                width="927"
                height="201"
                filterUnits="userSpaceOnUse"
                color-interpolation-filters="sRGB"
              >
                <feFlood flood-opacity="0" result="BackgroundImageFix" />
                <feColorMatrix
                  in="SourceAlpha"
                  type="matrix"
                  values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
                  result="hardAlpha"
                />
                <feMorphology
                  radius="10"
                  operator="dilate"
                  in="SourceAlpha"
                  result="effect1_dropShadow_21_23"
                />
                <feOffset dy="4" />
                <feGaussianBlur stdDeviation="2" />
                <feComposite in2="hardAlpha" operator="out" />
                <feColorMatrix type="matrix" values="0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.25 0" />
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_21_23" />
                <feBlend
                  mode="normal"
                  in="SourceGraphic"
                  in2="effect1_dropShadow_21_23"
                  result="shape"
                />
              </filter>
            </defs>
          </svg>
        </div>
        <h1>exploring the <span class="boxed pinkbox"> unknown </span></h1>
        <div class="oval bottomoval">
          <svg
            width="927"
            height="201"
            viewBox="0 0 927 201"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g filter="url(#filter0_d_21_23)">
              <ellipse cx="463.5" cy="96.5" rx="449.5" ry="86.5" fill="#FF63D3" />
            </g>
            <defs>
              <filter
                id="filter0_d_21_23"
                x="0"
                y="0"
                width="927"
                height="201"
                filterUnits="userSpaceOnUse"
                color-interpolation-filters="sRGB"
              >
                <feFlood flood-opacity="0" result="BackgroundImageFix" />
                <feColorMatrix
                  in="SourceAlpha"
                  type="matrix"
                  values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
                  result="hardAlpha"
                />
                <feMorphology
                  radius="10"
                  operator="dilate"
                  in="SourceAlpha"
                  result="effect1_dropShadow_21_23"
                />
                <feOffset dy="4" />
                <feGaussianBlur stdDeviation="2" />
                <feComposite in2="hardAlpha" operator="out" />
                <feColorMatrix type="matrix" values="0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.25 0" />
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_21_23" />
                <feBlend
                  mode="normal"
                  in="SourceGraphic"
                  in2="effect1_dropShadow_21_23"
                  result="shape"
                />
              </filter>
            </defs>
          </svg>
        </div>
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
  width: 25vw;
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
.redbox {
  background-color: #ff6363;
}
.orangebox {
  background-color: #ffae63;
}
.pinkbox {
  background-color: #ff63d3;
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
.arrow {
  position: relative;
  width: 100px;
  height: 100px;
}

.rightdown {
  /* bottom: 550px;
  left: 150px; */
}

.leftdown {
  /* bottom: 625px;
  left: 1525px; */
  transform: rotate(90deg);
}

.rightup {
  /* top: 625px;
  left: 150px; */
  transform: rotate(-90deg);
}

.leftup {
  /* top: 545px;
  left: 1500px; */
  transform: rotate(180deg);
}
.line-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px; /* Adjust the gap between lines if necessary */
  position: relative;
  top: 50px;
  right: 525px;
}

.line {
  display: flex;
  justify-content: center;
}

.topoval {
  position: relative;
  bottom: 100px;
  left: 850px;
}
.topoval svg {
  width: 927px;
  height: 201px;
}
.bottomoval {
  position: relative;
  top: 100px;
  left: 850px;
}
.bottomoval svg {
  width: 927px;
  height: 201px;
}
@media (min-width: 2400px) {
  .rightdown {
    bottom: 550px;
    left: 400px;
  }

  .leftdown {
    bottom: 625px;
    left: 1925px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 625px;
    left: 400px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 545px;
    left: 1925px;
    transform: rotate(180deg);
  }
  .line-container {
    right: 800px;
  }

  .topoval {
    position: relative;
    bottom: 100px;
    left: 1400px;
  }
  .topoval svg {
    width: 927px;
    height: 201px;
  }
  .bottomoval {
    position: relative;
    top: 100px;
    left: 1400px;
  }
  .bottomoval svg {
    width: 927px;
    height: 201px;
  }
}

@media (max-width: 2400px) and (min-width: 1800px) {
  .rightdown {
    bottom: 550px;
    left: 250px;
  }

  .leftdown {
    bottom: 625px;
    left: 1725px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 625px;
    left: 250px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 545px;
    left: 1725px;
    transform: rotate(180deg);
  }
  .topoval {
    position: relative;
    bottom: 100px;
    left: 1100px;
  }
  .topoval svg {
    width: 927px;
    height: 201px;
  }
  .bottomoval {
    position: relative;
    top: 100px;
    left: 1100px;
  }
  .bottomoval svg {
    width: 927px;
    height: 201px;
  }
}

@media (max-width: 1800px) and (min-width: 1600px) {
  .rightdown {
    bottom: 550px;
    left: 50px;
  }

  .leftdown {
    bottom: 625px;
    left: 1475px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 625px;
    left: 50px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 545px;
    left: 1475px;
    transform: rotate(180deg);
  }
  .topoval {
    position: relative;
    bottom: 100px;
    left: 800px;
  }
  .bottomoval {
    position: relative;
    top: 100px;
    left: 800px;
  }
}

@media (max-width: 1600px) and (min-width: 1380px) {
  .panel {
    font-size: 2.3vw;
  }
  .rightdown {
    bottom: 550px;
    left: 00px;
  }

  .leftdown {
    bottom: 625px;
    left: 1375px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 625px;
    left: 0px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 545px;
    left: 1375px;
    transform: rotate(180deg);
  }
  .line-container {
    right: 425px;
  }
  .topoval {
    position: relative;
    bottom: 100px;
    left: 500px;
  }
  .bottomoval {
    position: relative;
    top: 100px;
    left: 500px;
  }
}

@media (max-width: 1380px) and (min-width: 850px) {
  .panel {
    font-size: 2.2vw;
  }
  .star {
    width: 200px;
    height: 200px;
  }
  .arrow svg {
    width: 150px;
    height: 180px;
  }
  .rightdown {
    bottom: 450px;
    right: 150px;
  }
  .leftdown {
    bottom: 525px;
    left: 1000px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 525px;
    right: 150px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 445px;
    left: 1000px;
    transform: rotate(180deg);
  }
  .line-container {
    right: 275px;
  }
  .topoval {
    position: relative;
    bottom: 100px;
    left: 300px;
  }
  .topoval svg {
    width: 800px;
    height: 101px;
  }
  .bottomoval {
    position: relative;
    top: 100px;
    left: 300px;
  }
  .bottomoval svg {
    width: 800px;
    height: 101px;
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

  .arrow svg {
    width: 100px;
    height: 130px;
  }
  .rightdown {
    bottom: 350px;
    right: 160px;
  }
  .leftdown {
    bottom: 430px;
    left: 825px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 425px;
    right: 175px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 345px;
    left: 800px;
    transform: rotate(180deg);
  }
  .firstline svg {
    width: 50px;
  }
  .secondline svg {
    width: 100px;
  }
  .thirdline svg {
    width: 150px;
  }
  .fourthline svg {
    width: 200px;
  }
  .line-container {
    right: 190px;
    top: 25px;

    gap: 15px; /* Adjust the gap between lines if necessary */
  }
  .topoval {
    position: relative;
    bottom: 75px;
    left: 150px;
  }
  .topoval svg {
    width: 700px;
    height: 80px;
  }
  .bottomoval {
    position: relative;
    top: 75px;
    left: 150px;
  }
  .bottomoval svg {
    width: 700px;
    height: 80px;
  }
}
@media (max-width: 700px) and (min-width: 500px) {
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
  .arrow svg {
    width: 100px;
    height: 130px;
  }
  .rightdown {
    bottom: 350px;
    right: 300px;
  }
  .leftdown {
    bottom: 430px;
    left: 715px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 425px;
    right: 325px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 345px;
    left: 700px;
    transform: rotate(180deg);
  }
  .topoval {
    position: relative;
    bottom: 75px;
    left: 20px;
  }
  .topoval svg {
    width: 700px;
    height: 80px;
  }
  .bottomoval {
    position: relative;
    top: 75px;
    left: 20px;
  }
  .bottomoval svg {
    width: 700px;
    height: 80px;
  }
}
@media (max-width: 500px) {
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
  .arrow svg {
    width: 100px;
    height: 130px;
  }
  .rightdown {
    bottom: 350px;
    right: 350px;
  }
  .leftdown {
    bottom: 430px;
    left: 665px;
    transform: rotate(90deg);
  }

  .rightup {
    top: 425px;
    right: 375px;
    transform: rotate(-90deg);
  }

  .leftup {
    top: 345px;
    left: 650px;
    transform: rotate(180deg);
  }
  .firstline svg {
    width: 25px;
  }
  .secondline svg {
    width: 75px;
  }
  .thirdline svg {
    width: 125px;
  }
  .fourthline svg {
    width: 175px;
  }
  .line-container {
    right: 110px;
    top: 15px;

    gap: 5px; /* Adjust the gap between lines if necessary */
  }
  .topoval {
    position: relative;
    bottom: 50px;
    left: -20px;
  }
  .topoval svg {
    width: 600px;
    height: 50px;
  }
  .bottomoval {
    position: relative;
    top: 50px;
    left: -20px;
  }
  .bottomoval svg {
    width: 600px;
    height: 50px;
  }
}
</style>
