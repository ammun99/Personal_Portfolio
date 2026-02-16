<template>
  <section ref="section" id="about" class="bg-gray-950 text-white px-6 py-24">
    <div class="max-w-6xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-10 items-start">
      <div>
        <p class="text-sm tracking-widest text-gray-400 uppercase">About</p>
        <h2 ref="title" class="text-3xl md:text-4xl font-bold mt-3">
          Building clean UI + solid systems behind it.
        </h2>
        <p ref="body" class="text-gray-300 mt-4 leading-relaxed max-w-xl">
          I’m Amrutha — a software engineer who loves building modern, interactive web experiences.
          I work across frontend and backend, and I’m comfortable connecting Vue applications to Python services
          (FastAPI) and production databases.
        </p>

        <div ref="links" class="mt-6 flex flex-wrap gap-3">
          <a
            class="px-4 py-2 rounded-xl bg-white/5 border border-white/10 hover:bg-white/10 transition"
            href="https://github.com/ammun99"
            target="_blank"
            rel="noreferrer"
          >
            GitHub ↗
          </a>
          <a
            class="px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-500 transition"
            href="#contact"
          >
            Work with me
          </a>
        </div>
      </div>

      <div ref="cards" class="grid grid-cols-1 sm:grid-cols-2 gap-4">
        <div
          class="rounded-2xl border border-white/10 bg-white/5 p-5
                 hover:bg-white/10 hover:scale-[1.02] transition duration-300"
        >
          <p class="text-3xl font-bold text-indigo-300">{{ years }}+</p>
          <p class="text-gray-300 mt-2">Years building full-stack projects</p>
        </div>

        <div
          class="rounded-2xl border border-white/10 bg-white/5 p-5
                 hover:bg-white/10 hover:scale-[1.02] transition duration-300"
        >
          <p class="text-3xl font-bold text-indigo-300">{{ apis }}+</p>
          <p class="text-gray-300 mt-2">APIs built (secure + scalable)</p>
        </div>

        <div
          class="rounded-2xl border border-white/10 bg-white/5 p-5
                 hover:bg-white/10 hover:scale-[1.02] transition duration-300"
        >
          <p class="text-3xl font-bold text-indigo-300">{{ llm }}</p>
          <p class="text-gray-300 mt-2">RAG + knowledge graph experience</p>
        </div>

        <div
          class="rounded-2xl border border-white/10 bg-white/5 p-5
                 hover:bg-white/10 hover:scale-[1.02] transition duration-300"
        >
          <p class="text-3xl font-bold text-indigo-300">{{ vueLabel }}</p>
          <p class="text-gray-300 mt-2">Component-first UI engineering</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue"
import { gsap } from "gsap"

const section = ref(null)
const title = ref(null)
const body = ref(null)
const links = ref(null)
const cards = ref(null)

const years = ref(0)
const apis = ref(0)
const llm = ref("")
const vueLabel = ref("")

function animateNumber(refVar, to, duration = 900) {
  const from = 0
  const start = performance.now()

  function tick(now) {
    const progress = Math.min((now - start) / duration, 1)
    // easeOutCubic for a smoother "premium" count
    const eased = 1 - Math.pow(1 - progress, 3)
    refVar.value = Math.floor(from + (to - from) * eased)
    if (progress < 1) requestAnimationFrame(tick)
  }

  requestAnimationFrame(tick)
}

let observer
let played = false

onMounted(() => {
  const animateIn = () => {
    const ctx = gsap.context(() => {
      gsap.from(title.value, { opacity: 0, y: 14, duration: 0.6, clearProps: "all" })
      gsap.from(body.value, { opacity: 0, y: 12, duration: 0.6, delay: 0.12, clearProps: "all" })
      gsap.from(links.value, { opacity: 0, y: 10, duration: 0.5, delay: 0.2, clearProps: "all" })

      const items = cards.value ? Array.from(cards.value.children) : []
      gsap.from(items, {
        opacity: 0,
        y: 14,
        stagger: 0.12,
        duration: 0.55,
        delay: 0.25,
        clearProps: "all",
      })
    })

    // Counters trigger once
    animateNumber(years, 3, 900)
    animateNumber(apis, 20, 1100)
    setTimeout(() => (llm.value = "LLM"), 200)
    setTimeout(() => (vueLabel.value = "Vue"), 350)

    observer?.disconnect()
    return () => ctx.revert()
  }

  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting && !played) {
        played = true
        animateIn()
      }
    },
    { threshold: 0.2 }
  )

  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => {
  observer?.disconnect()
})
</script>
