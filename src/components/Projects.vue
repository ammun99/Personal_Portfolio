<template>
  <section ref="section" id="projects" class="bg-gray-950 text-white px-6 py-24">
    <div class="max-w-6xl mx-auto">
      <div class="flex items-end justify-between gap-6 flex-wrap">
        <div>
          <h2 ref="title" class="text-3xl md:text-4xl font-bold">Projects</h2>
          <p ref="subtitle" class="text-gray-300 mt-3 max-w-2xl">
            A few things I’ve built using Vue, JavaScript, and Python-friendly backends.
          </p>
        </div>

        <a
          ref="cta"
          class="inline-flex items-center gap-2 text-sm px-4 py-2 rounded-xl border border-white/10
                 bg-white/5 hover:bg-white/10 transition"
          href="https://github.com/ammun99"
          target="_blank"
          rel="noreferrer"
        >
          GitHub ↗
        </a>
      </div>

      <div ref="grid" class="mt-10 grid grid-cols-1 md:grid-cols-2 gap-6">
        <article
          v-for="p in projects"
          :key="p.title"
          class="group rounded-2xl border border-white/10 bg-white/5 p-6
                 hover:bg-white/10 transition duration-200
                 hover:-translate-y-1 hover:border-white/20"
        >
          <div
          class="tilt-card rounded-2xl border border-white/10 bg-white/5 p-6 hover:bg-white/10 transition"
          @mousemove="onTiltMove"
          @mouseleave="onTiltLeave">

            <h3 class="text-xl font-semibold group-hover:text-indigo-300 transition">
              {{ p.title }}
            </h3>
            <span class="text-xs text-gray-400 border border-white/10 rounded-full px-2 py-1">
              {{ p.type }}
            </span>
          </div>

          <p class="text-gray-300 mt-3 leading-relaxed">
            {{ p.description }}
          </p>

          <div class="mt-4 flex flex-wrap gap-2">
            <span
              v-for="t in p.tech"
              :key="t"
              class="text-xs px-3 py-1 rounded-full border border-white/10 bg-black/20 text-gray-200"
            >
              {{ t }}
            </span>
          </div>

          <div class="mt-6 flex items-center gap-3">
            <a
              v-if="p.demo"
              :href="p.demo"
              target="_blank"
              rel="noreferrer"
              class="text-sm px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-500 transition"
            >
              Live Demo
            </a>
            <a
              v-if="p.code"
              :href="p.code"
              target="_blank"
              rel="noreferrer"
              class="text-sm px-4 py-2 rounded-xl border border-white/10 bg-white/0 hover:bg-white/5 transition"
            >
              Code
            </a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue"
import { gsap } from "gsap"

const title = ref(null)
const subtitle = ref(null)
const cta = ref(null)
const grid = ref(null)
const section = ref(null)
function onTiltMove(e) {
  const card = e.currentTarget
  const rect = card.getBoundingClientRect()

  const x = e.clientX - rect.left
  const y = e.clientY - rect.top

  const cx = rect.width / 2
  const cy = rect.height / 2

  const dx = (x - cx) / cx
  const dy = (y - cy) / cy

  const maxTilt = 10 // keep subtle (degrees)
  const rotateY = dx * maxTilt
  const rotateX = -dy * maxTilt

  card.style.transform = `perspective(900px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateY(-2px)`
}

function onTiltLeave(e) {
  const card = e.currentTarget
  card.style.transform = `perspective(900px) rotateX(0deg) rotateY(0deg) translateY(0px)`
}


// Replace these with your real projects next — keep 3–4 max on homepage
const projects = [
  {
  title: "Flappy Bird Clone",
  type: "Game Development",
  description:
    "Developed a 2D Bird-style arcade game in Java featuring physics-based bird movement, real-time collision detection, procedural obstacle generation, and event-driven gameplay using Swing graphics.",
  tech: ["Java", "Swing", "AWT", "Object-Oriented Programming", "Game Loop Architecture"],
  demo: "",
  code: "https://github.com/ammun99/Bird_Game",
},

  {
    title: "LLM Fault Detection System",
    type: "AI / NLP",
    description:
      "Designed an LLM-powered maintenance assistant using RAG + knowledge graphs to classify faults and recommend resolutions.",
    tech: ["RAG", "Neo4j", "Python", "LLMs"],
    demo: "",
    code: "",
  },
  {
    title: "SEO Analytics Dashboard",
    type: "Frontend + API",
    description:
      "ETL pipeline + dashboard to visualize Search Console metrics with a clean UI and filterable charts.",
    tech: ["Vue", "Express", "MySQL", "APIs"],
    demo: "",
    code: "",
  },
  {
  title: "Portfolio (Vue + Tailwind)",
  type: "Frontend",
  description:
    "Designed and built a fully interactive portfolio using Vue 3, Tailwind CSS, and GSAP animations. Implements component-driven architecture, scroll-triggered animations, and responsive UI patterns.",
  tech: ["Vue 3", "Tailwind", "GSAP"],
  demo: "https://ammun99.github.io/Portfolio/",
  code: "https://github.com/ammun99/Portfolio",
},
]

let observer

onMounted(() => {
  const animateIn = () => {
    const ctx = gsap.context(() => {
      gsap.from(title.value, { opacity: 0, y: 12, duration: 0.5, clearProps: "all" })
      gsap.from(subtitle.value, { opacity: 0, y: 10, duration: 0.5, delay: 0.12, clearProps: "all" })
      gsap.from(cta.value, { opacity: 0, y: 10, duration: 0.4, delay: 0.18, clearProps: "all" })

      const cards = grid.value ? Array.from(grid.value.children) : []
      gsap.from(cards, {
        opacity: 0,
        y: 16,
        stagger: 0.12,
        duration: 0.6,
        delay: 0.2,
        clearProps: "all",
      })
    })

    // prevent re-animating repeatedly
    observer?.disconnect()

    return () => ctx.revert()
  }

  observer = new IntersectionObserver(
    (entries) => {
      const entry = entries[0]
      if (entry.isIntersecting) animateIn()
    },
    { threshold: 0.2 }
  )

  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => {
  observer?.disconnect()
})


</script>
<style scoped>
.tilt-card {
  transform-style: preserve-3d;
  transition: transform 180ms ease, background 200ms ease, border-color 200ms ease;
  will-change: transform;
}
</style>

