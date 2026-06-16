<script setup>
import { onMounted, onUnmounted } from 'vue'

let cleanup = () => {}

onMounted(() => {
  const clamp = (value, min = 0, max = 1) => Math.min(Math.max(value, min), max)
  const root = document.documentElement
  const scenes = [...document.querySelectorAll('.scene')]
  const heroScene = document.querySelector('.hero')
  const thesisScene = document.querySelector('.thesis')
  const systemsScene = document.querySelector('.systems')
  const missionsScene = document.querySelector('.missions')
  const cutawayScene = document.querySelector('.cutaway')
  const hudLabel = document.getElementById('hudLabel')
  const hudPct = document.getElementById('hudPct')
  const cursor = document.querySelector('.cursor')
  const diagramPaths = [...document.querySelectorAll('.diagram path')]
  const map = document.getElementById('map')
  const mapLines = document.getElementById('mapLines')
  const nodes = [...document.querySelectorAll('.node')]
  const commandLinks = [...document.querySelectorAll('.commands a')]
  const hoverTargets = [...document.querySelectorAll('a, button, .node')]
  const revealTargets = [...document.querySelectorAll('.reveal, .log')]
  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)')
  const mobileLayout = window.matchMedia('(max-width: 680px)')
  let ticking = false
  let pointerFrame = 0
  let pointerX = '50vw'
  let pointerY = '50vh'
  let lineElements = []
  let revealObserver

  const progressFor = (element) => {
    if (!element) return 0
    const rect = element.getBoundingClientRect()
    const distance = rect.height - window.innerHeight

    if (distance <= 0) {
      return rect.top < window.innerHeight && rect.bottom > 0 ? 1 : 0
    }

    return clamp(-rect.top / distance)
  }

  const pageProgress = () => {
    const max = document.documentElement.scrollHeight - window.innerHeight
    return max <= 0 ? 0 : window.scrollY / max
  }

  const activeScene = () => {
    let active = scenes[0]
    let min = Infinity

    for (const scene of scenes) {
      const rect = scene.getBoundingClientRect()
      const distance = Math.abs(rect.top)

      if (
        rect.top <= window.innerHeight * 0.58 &&
        rect.bottom >= window.innerHeight * 0.24 &&
        distance < min
      ) {
        active = scene
        min = distance
      }
    }

    return active
  }

  const initPaths = () => {
    diagramPaths.forEach((path) => {
      const length = path.getTotalLength ? path.getTotalLength() : 1
      path.dataset.len = length
      path.style.strokeDasharray = length
      path.style.strokeDashoffset = length
    })
  }

  const initMapLines = () => {
    if (!mapLines || lineElements.length) return
    lineElements = nodes
      .filter((node) => node.dataset.node !== 'core')
      .map(() => {
        const line = document.createElementNS('http://www.w3.org/2000/svg', 'line')
        mapLines.appendChild(line)
        return line
      })
  }

  const setStaticMotion = () => {
    root.style.setProperty('--page-p', '1')
    root.style.setProperty('--hero-p', '1')
    root.style.setProperty('--thesis-p', '1')
    root.style.setProperty('--map-p', '1')
    root.style.setProperty('--mission-p', '0')
    root.style.setProperty('--cutaway-p', '1')

    diagramPaths.forEach((path) => {
      path.style.strokeDashoffset = '0'
    })

    revealTargets.forEach((element) => element.classList.add('is-visible'))
    setMapNodes(1)
  }

  const setMapNodes = (progress) => {
    if (!map || mobileLayout.matches) return

    const rect = map.getBoundingClientRect()
    const width = rect.width || 1000
    const height = rect.height || 700
    const centerX = width / 2
    const centerY = height / 2
    const radiusX = Math.min(width * 0.36, 340)
    const radiusY = Math.min(height * 0.32, 230)
    const data = {
      core: [centerX, centerY],
      cloud: [
        centerX + Math.cos(-1.55 + progress * 0.4) * radiusX,
        centerY + Math.sin(-1.55 + progress * 0.4) * radiusY
      ],
      obs: [
        centerX + Math.cos(-0.52 + progress * 0.25) * radiusX,
        centerY + Math.sin(-0.52 + progress * 0.25) * radiusY
      ],
      auto: [
        centerX + Math.cos(0.48 - progress * 0.3) * radiusX,
        centerY + Math.sin(0.48 - progress * 0.3) * radiusY
      ],
      front: [
        centerX + Math.cos(1.55 + progress * 0.2) * radiusX,
        centerY + Math.sin(1.55 + progress * 0.2) * radiusY
      ],
      product: [
        centerX + Math.cos(2.55 - progress * 0.25) * radiusX,
        centerY + Math.sin(2.55 - progress * 0.25) * radiusY
      ],
      risk: [
        centerX + Math.cos(3.55 + progress * 0.3) * radiusX,
        centerY + Math.sin(3.55 + progress * 0.3) * radiusY
      ]
    }
    const chaos = (1 - progress) * 170

    nodes.forEach((node, index) => {
      const key = node.dataset.node
      const point = data[key]
      if (!point) return
      const [x, y] = point
      const jitterX = Math.sin(index * 10.2) * chaos
      const jitterY = Math.cos(index * 7.7) * chaos
      node.style.left = x + jitterX + 'px'
      node.style.top = y + jitterY + 'px'
      node.style.opacity = String(0.35 + progress * 0.65)
      node.style.transform =
        'translate(-50%, -50%) rotate(' + (1 - progress) * Math.sin(index) * 9 + 'deg)'
    })

    const core = data.core
    let lineIndex = 0
    Object.entries(data).forEach(([key, point]) => {
      if (key === 'core') return
      const line = lineElements[lineIndex]
      lineIndex += 1
      if (!line) return
      line.setAttribute('x1', String((core[0] / width) * 1000))
      line.setAttribute('y1', String((core[1] / height) * 700))
      line.setAttribute('x2', String((point[0] / width) * 1000))
      line.setAttribute('y2', String((point[1] / height) * 700))
      line.style.opacity = String(clamp((progress - 0.18) / 0.6))
    })
  }

  const update = () => {
    ticking = false
    const pp = pageProgress()
    root.style.setProperty('--page-p', pp.toFixed(4))

    if (hudPct)
      hudPct.textContent =
        Math.round(pp * 100)
          .toString()
          .padStart(2, '0') + '%'
    if (hudLabel) hudLabel.textContent = activeScene()?.dataset.label || 'LIVE DOSSIER'

    const heroP = progressFor(heroScene)
    const thesisP = progressFor(thesisScene)
    const mapP = progressFor(systemsScene)
    const missionP = progressFor(missionsScene)
    const cutawayP = progressFor(cutawayScene)
    root.style.setProperty('--hero-p', heroP.toFixed(4))
    root.style.setProperty('--thesis-p', thesisP.toFixed(4))
    root.style.setProperty('--map-p', mapP.toFixed(4))
    root.style.setProperty('--mission-p', missionP.toFixed(4))
    root.style.setProperty('--cutaway-p', cutawayP.toFixed(4))

    diagramPaths.forEach((path, index) => {
      const length = Number(path.dataset.len || 1)
      const local = clamp((thesisP - index * 0.055) / 0.72)
      path.style.strokeDashoffset = String(length * (1 - local))
    })

    setMapNodes(mapP)
  }

  const requestUpdate = () => {
    if (reduceMotion.matches) return
    if (!ticking) {
      ticking = true
      requestAnimationFrame(update)
    }
  }

  revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) entry.target.classList.add('is-visible')
      })
    },
    { threshold: 0.18 }
  )

  revealTargets.forEach((element) => revealObserver.observe(element))

  const onPointerMove = (event) => {
    if (reduceMotion.matches) return
    pointerX = event.clientX + 'px'
    pointerY = event.clientY + 'px'

    if (!pointerFrame) {
      pointerFrame = requestAnimationFrame(() => {
        pointerFrame = 0
        root.style.setProperty('--mx', pointerX)
        root.style.setProperty('--my', pointerY)
      })
    }
  }

  const onMouseEnter = () => cursor?.classList.add('is-hovering')
  const onMouseLeave = () => cursor?.classList.remove('is-hovering')
  hoverTargets.forEach((element) => {
    element.addEventListener('mouseenter', onMouseEnter)
    element.addEventListener('mouseleave', onMouseLeave)
  })

  const commandHandlers = commandLinks.map((link) => {
    const move = (event) => {
      if (reduceMotion.matches || mobileLayout.matches) return
      const rect = link.getBoundingClientRect()
      const x = (event.clientX - rect.left - rect.width / 2) * 0.08
      const y = (event.clientY - rect.top - rect.height / 2) * 0.18
      link.style.transform = 'translate(' + x + 'px, ' + y + 'px)'
    }
    const leave = () => {
      link.style.transform = 'translate(0, 0)'
    }
    link.addEventListener('pointermove', move)
    link.addEventListener('pointerleave', leave)
    return { link, move, leave }
  })

  const onResize = () => {
    requestUpdate()
  }

  window.addEventListener('pointermove', onPointerMove, { passive: true })
  window.addEventListener('scroll', requestUpdate, { passive: true })
  window.addEventListener('resize', onResize)

  initPaths()
  initMapLines()
  if (reduceMotion.matches) {
    setStaticMotion()
  } else {
    update()
  }

  cleanup = () => {
    revealObserver?.disconnect()
    window.removeEventListener('pointermove', onPointerMove)
    window.removeEventListener('scroll', requestUpdate)
    window.removeEventListener('resize', onResize)
    if (pointerFrame) cancelAnimationFrame(pointerFrame)
    hoverTargets.forEach((element) => {
      element.removeEventListener('mouseenter', onMouseEnter)
      element.removeEventListener('mouseleave', onMouseLeave)
    })
    commandHandlers.forEach(({ link, move, leave }) => {
      link.removeEventListener('pointermove', move)
      link.removeEventListener('pointerleave', leave)
    })
  }
})

onUnmounted(() => {
  cleanup()
})
</script>

<template>
  <div class="cursor" aria-hidden="true"></div>

  <aside class="hud" aria-label="Site status">
    <div class="hud__brand"><span>R / DESAI</span></div>
    <div class="hud__rail"><span></span></div>
    <div class="hud__right">
      <span id="hudLabel">BOOT SEQUENCE</span> · <span id="hudPct">00%</span>
    </div>
  </aside>

  <main>
    <section class="hero scene" data-label="BOOT SEQUENCE">
      <div class="sticky hero__stage">
        <div class="hero__scan" aria-hidden="true"></div>
        <div class="hero__orbit" aria-hidden="true"><i class="hero__dot"></i></div>
        <div class="hero__content">
          <div>
            <div class="hero__kicker grain-label">
              <i></i><span>personal systems dossier / Chicago IL</span>
            </div>
            <h1 aria-label="Rohan Desai"><span>Rohan</span><span>Desai</span></h1>
            <div class="hero__subline">
              <p>
                Software engineer working across infrastructure, cloud, AI, research systems, and
                founder-led product work from Chicago.
              </p>
              <p>
                I like the messy middle: turning slow internal workflows, unreliable signals, and
                ambiguous product ideas into systems people can actually use.
              </p>
            </div>
          </div>
          <aside class="console" aria-label="Boot console">
            <div class="console__top">
              <span>kernel: rohan-desai</span><span>status: live</span>
            </div>
            <p>loading developer profile</p>
            <p class="blue">indexing cloud and infra work</p>
            <p>hydrating saas / ai / research layer</p>
            <p class="warn">checking edge cases</p>
            <p>ready to build</p>
          </aside>
        </div>
        <p class="corner-copy">
          Chicago, IL / University of Michigan / software engineer, founder, systems builder.
        </p>
      </div>
    </section>

    <section class="thesis scene" data-label="SIGNAL OVER NOISE">
      <div class="sticky thesis__stage">
        <span class="section-index">01 / signal over noise</span>
        <div class="thesis__copy reveal">
          <h2><span>Build systems.</span><span>Reduce noise.</span><span>Ship leverage.</span></h2>
          <p>
            I gravitate toward work with unclear edges: infrastructure requests stuck in queues,
            telemetry that disappears at the edge, research workflows with real money attached, and
            products that need both taste and operational discipline.
          </p>
        </div>
        <div class="diagram" aria-label="Animated architecture diagram">
          <svg viewBox="0 0 900 700" preserveAspectRatio="none" aria-hidden="true">
            <path class="hot" d="M80,350 C210,140 310,120 440,310 S680,520 820,260" />
            <path class="blue" d="M120,110 C260,280 380,290 510,190 S690,90 780,180" />
            <path class="orange" d="M160,600 C250,420 390,490 470,390 S620,300 760,570" />
            <path d="M80,470 C230,530 340,210 470,330 S690,420 830,390" />
            <path d="M260,70 L260,650 M450,70 L450,650 M640,70 L640,650" />
            <path d="M70,230 L830,230 M70,430 L830,430" />
          </svg>
          <div class="diagram__tag">platform layer</div>
          <div class="diagram__tag">runtime signals</div>
          <div class="diagram__tag">operator mindset</div>
        </div>
      </div>
    </section>

    <section class="systems scene" data-label="SYSTEMS MAP">
      <div class="sticky systems__stage">
        <aside class="systems__aside reveal">
          <span class="grain-label">02 / systems map</span>
          <h2>Not skills. Operating range.</h2>
          <p>
            TypeScript, Python, SQL, Bash, Kubernetes, OpenShift, AWS, Azure, Terraform, PostgreSQL,
            React, Next.js, Vue, React Native, OpenTelemetry, Grafana, OpenSearch, and the OpenAI
            API.
          </p>
          <div class="systems__metrics">
            <span><b>mode</b><em>hands-on builder</em></span>
            <span><b>range</b><em>infra to product</em></span>
            <span><b>style</b><em>curious, direct, high-agency</em></span>
          </div>
        </aside>
        <div class="map" id="map">
          <svg
            id="mapLines"
            viewBox="0 0 1000 700"
            preserveAspectRatio="none"
            aria-hidden="true"
          ></svg>
          <div class="node node--core" data-node="core">
            <div><b>Rohan</b><small>infra / product</small></div>
          </div>
          <div class="node" data-node="cloud">
            <b>Cloud Platforms</b><small>OpenShift / K8s</small>
          </div>
          <div class="node" data-node="obs"><b>Observability</b><small>OTel / Grafana</small></div>
          <div class="node" data-node="auto">
            <b>Automation</b><small>Actions / ServiceNow</small>
          </div>
          <div class="node" data-node="front">
            <b>Product Surfaces</b><small>React / Vue / RN</small>
          </div>
          <div class="node" data-node="product"><b>AI Workflows</b><small>RAG / agents</small></div>
          <div class="node" data-node="risk">
            <b>Research Systems</b><small>models / payouts</small>
          </div>
        </div>
      </div>
    </section>

    <section class="missions scene" data-label="MISSIONS">
      <div class="sticky missions__stage">
        <div class="missions__head">
          <span class="grain-label">03 / work as missions</span>
          <h2>Field work.</h2>
        </div>
        <div class="mission-track">
          <article class="mission" data-no="01">
            <div class="mission__copy">
              <span class="grain-label">mission 01 / BNSF Railway</span>
              <h3>Infra unlocked</h3>
              <p>
                Automated OpenShift namespace and quota provisioning from a three-day wait to under
                five minutes, handling roughly 50 developer requests a month with GitHub Actions,
                Python, Bash, and ServiceNow.
              </p>
              <div class="mission__meta">
                <span>openshift</span><span>python</span><span>servicenow</span>
              </div>
            </div>
            <div class="payload">
              <div class="payload__header">
                <span>active role</span>
                <b>Software Engineer, Infrastructure & Cloud</b>
              </div>
              <div class="payload__metrics">
                <span><b>~3 days</b><small>to under 5 min</small></span>
                <span><b>~50</b><small>requests / month</small></span>
                <span><b>11</b><small>clusters instrumented</small></span>
              </div>
              <div class="payload__grid">
                <div class="payload__group">
                  <span>owned</span>
                  <ul>
                    <li>OpenShift namespace and quota automation</li>
                    <li>ServiceNow-backed request and approval flow</li>
                    <li>OpenTelemetry, Grafana, and OpenSearch rollout</li>
                    <li>Incident creation with team and severity routing</li>
                  </ul>
                </div>
                <div class="payload__group">
                  <span>additional systems</span>
                  <ul>
                    <li>Store-and-forward telemetry for edge rail-car Kubernetes clusters</li>
                    <li>Wiki.js rollout for 600 users, saving about $100K/year</li>
                    <li>Azure FinOps inventory across roughly $1M/month in spend</li>
                  </ul>
                </div>
              </div>
              <div class="payload__stack">
                <span>OpenShift</span><span>Python</span><span>Bash</span><span>ServiceNow</span
                ><span>OpenTelemetry</span><span>Azure</span>
              </div>
            </div>
          </article>
          <article class="mission" data-no="02">
            <div class="mission__copy">
              <span class="grain-label">mission 02 / Syntrek</span>
              <h3>Zero to beta</h3>
              <p>
                Founded and built a multi-tenant B2B SaaS platform for industrial safety and
                compliance across backend, web, mobile, database, cloud infrastructure, CI/CD, and
                customer workflows.
              </p>
              <div class="mission__meta">
                <span>typescript</span><span>postgresql</span><span>aws</span>
              </div>
            </div>
            <div class="payload">
              <div class="payload__header">
                <span>founder track</span>
                <b>Production-grade B2B SaaS from zero to beta</b>
              </div>
              <div class="payload__metrics">
                <span><b>sole</b><small>engineer</small></span>
                <span><b>multi</b><small>tenant platform</small></span>
                <span><b>web + mobile</b><small>customer workflows</small></span>
              </div>
              <div class="payload__grid">
                <div class="payload__group">
                  <span>built</span>
                  <ul>
                    <li>Backend, web app, mobile app, database, and cloud infrastructure</li>
                    <li>Tenant isolation, RBAC, audit logging, and shared types</li>
                    <li>Offline-first mobile sync, background jobs, and real-time updates</li>
                    <li>Staging/production environments, rollback procedures, and backups</li>
                  </ul>
                </div>
                <div class="payload__group">
                  <span>operator work</span>
                  <ul>
                    <li>Product discovery and beta workflow validation</li>
                    <li>User outreach, roadmap prioritization, and compliance domain research</li>
                    <li>AI-assisted development workflow with review gates and regression tests</li>
                  </ul>
                </div>
              </div>
              <div class="payload__stack">
                <span>TypeScript</span><span>Node.js</span><span>Next.js</span
                ><span>React Native</span><span>PostgreSQL</span><span>AWS</span
                ><span>Terraform</span>
              </div>
            </div>
          </article>
          <article class="mission" data-no="03">
            <div class="mission__copy">
              <span class="grain-label">mission 03 / CLUES</span>
              <h3>Context for learning</h3>
              <p>
                Contributed to a RAG-based AI learning platform using the OpenAI API to ingest
                course material and generate study guides, explanations, and practice content for
                university students.
              </p>
              <div class="mission__meta">
                <span>openai api</span><span>rag</span><span>education</span>
              </div>
            </div>
            <div class="payload">
              <div class="payload__header">
                <span>AI learning system</span>
                <b>Contextual Linkages for Undergraduate Education</b>
              </div>
              <div class="payload__metrics">
                <span><b>RAG</b><small>course material ingestion</small></span>
                <span><b>OpenAI</b><small>study generation</small></span>
                <span><b>5-8%</b><small>grade improvement</small></span>
              </div>
              <div class="payload__grid">
                <div class="payload__group">
                  <span>contributed</span>
                  <ul>
                    <li>Course-aware study guides, explanations, and practice content</li>
                    <li>Relevant retrieval over course materials and structured context</li>
                    <li>Student-facing AI workflows tuned for clarity and usefulness</li>
                  </ul>
                </div>
                <div class="payload__group">
                  <span>focus</span>
                  <ul>
                    <li>Making AI output specific to the class, not generic tutoring copy</li>
                    <li>Keeping the product practical for student use during actual coursework</li>
                    <li>Bridging research ideas with a usable learning surface</li>
                  </ul>
                </div>
              </div>
              <div class="payload__stack">
                <span>OpenAI API</span><span>RAG</span><span>course data</span
                ><span>education</span>
              </div>
            </div>
          </article>
          <article class="mission" data-no="04">
            <div class="mission__copy">
              <span class="grain-label">mission 04 / research + markets</span>
              <h3>Modeled behavior</h3>
              <p>
                Built behavioral economics games studying cooperation and decision-making, then
                applied the same modeling instinct to a Python/Selenium market inefficiency scanner.
              </p>
              <div class="mission__meta">
                <span>python</span><span>selenium</span><span>game theory</span>
              </div>
            </div>
            <div class="payload">
              <div class="payload__header">
                <span>research + markets</span>
                <b>Behavioral games and inefficiency scanning</b>
              </div>
              <div class="payload__metrics">
                <span><b>2023-25</b><small>lab research</small></span>
                <span><b>real $</b><small>payout models</small></span>
                <span><b>~$400/mo</b><small>scanner output</small></span>
              </div>
              <div class="payload__grid">
                <div class="payload__group">
                  <span>modeled</span>
                  <ul>
                    <li>
                      Original behavioral economics games for cooperation and altruism research
                    </li>
                    <li>Game mechanics, mathematical outcomes, and real-money payout structures</li>
                    <li>Group decision-making scenarios supporting PhD research</li>
                  </ul>
                </div>
                <div class="payload__group">
                  <span>built</span>
                  <ul>
                    <li>Python/Selenium scanner for live pricing discrepancies</li>
                    <li>Expected-value comparison logic for market inefficiency detection</li>
                    <li>Automation workflow that produced about $400/month during active use</li>
                  </ul>
                </div>
              </div>
              <div class="payload__stack">
                <span>Python</span><span>Selenium</span><span>game theory</span
                ><span>EV models</span>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section class="cutaway scene" data-label="ARCHITECTURE CUTAWAY">
      <div class="sticky cutaway__stage">
        <div class="reveal">
          <span class="grain-label">04 / architecture cutaway</span>
          <h2>Layer by layer.</h2>
          <p>
            I am comfortable owning the boring parts that make software real: identity, data models,
            deployment paths, observability, rollback plans, security hardening, and the user
            workflow sitting on top.
          </p>
        </div>
        <div class="stack" aria-label="Animated architecture stack">
          <div class="stack__beam"></div>
          <div class="layer"><span>Web / mobile surface</span><i></i></div>
          <div class="layer"><span>API and workflow layer</span><i></i></div>
          <div class="layer"><span>Tenant isolation / RBAC</span><i></i></div>
          <div class="layer"><span>PostgreSQL / Redis data plane</span><i></i></div>
          <div class="layer"><span>Telemetry / incident automation</span><i></i></div>
          <div class="layer"><span>Terraform / Docker / CI-CD</span><i></i></div>
        </div>
      </div>
    </section>

    <section class="proof scene" data-label="PROOF STREAM">
      <h2 class="reveal">Proof stream.</h2>
      <div class="proof-stream">
        <article class="log">
          <time>[2025]</time>
          <div>
            <b>Provisioning delay cut from about 3 days to under 5 minutes</b>
            <p>
              Automated OpenShift namespace and quota requests at BNSF with GitHub Actions, Python,
              Bash, and ServiceNow.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2025]</time>
          <div>
            <b>Observability across 11 clusters and 8 internal orgs</b>
            <p>
              Deployed OpenTelemetry and open-source exporters across OpenShift, Nutanix,
              VMware/vCenter, and storage estates.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2025]</time>
          <div>
            <b>Wiki.js rollout for 600 users, saving about $100K/year</b>
            <p>Owned VM provisioning, auth, security, rollout, and migration tooling end to end.</p>
          </div>
        </article>
        <article class="log">
          <time>[2025]</time>
          <div>
            <b>FinOps inventory across roughly $1M/month in Azure spend</b>
            <p>Identified unused resources that enabled teams to cut about $20K/month in waste.</p>
          </div>
        </article>
        <article class="log">
          <time>[2025]</time>
          <div>
            <b>Syntrek built from zero to beta as founder and sole engineer</b>
            <p>
              Built multi-tenant SaaS foundations across Node.js, Next.js, React Native, AWS, and
              Terraform.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2024]</time>
          <div>
            <b>AI training platform features across 6 production release cycles</b>
            <p>
              Built Vue.js frontend work at 24G with REST APIs and specialized knowledge-base flows.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2024]</time>
          <div>
            <b>CLUES users saw roughly 5-8% course grade improvement</b>
            <p>
              Helped build RAG-based study generation using course materials and the OpenAI API.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2023-25]</time>
          <div>
            <b>Behavioral economics games with real-money payout structures</b>
            <p>
              Modeled game mechanics and mathematical outcomes for research on cooperation,
              altruism, and group decision-making.
            </p>
          </div>
        </article>
        <article class="log">
          <time>[2023]</time>
          <div>
            <b>Market scanner produced about $400/month during active use</b>
            <p>
              Scraped live pricing data with Python/Selenium and compared expected-value
              opportunities.
            </p>
          </div>
        </article>
      </div>
    </section>

    <section class="final scene" data-label="HANDOFF">
      <div class="final__inner">
        <div>
          <span class="grain-label">05 / handoff</span>
          <h2>Let’s talk systems.</h2>
        </div>
        <nav class="commands" aria-label="Contact links">
          <a
            href="https://www.linkedin.com/in/rohan-desai-2a4b6b22a"
            target="_blank"
            rel="noreferrer"
            >open linkedin</a
          >
          <a href="https://github.com/Rohan-Desai" target="_blank" rel="noreferrer"
            >inspect github</a
          >
          <a href="mailto:rohanndesai03@gmail.com">send email</a>
          <a href="tel:+15862758966">call rohan</a>
        </nav>
      </div>
    </section>
  </main>
</template>
