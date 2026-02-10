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
        <div class="rounded-2xl border border-white/10 bg-white/5 p-5 hover:bg-white/10 transition">
          <p class="text-3xl font-bold text-indigo-300">3+</p>
          <p class="text-gray-300 mt-2">Years building full-stack projects</p>
        </div>

        <div class="rounded-2xl border border-white/10 bg-white/5 p-5 hover:bg-white/10 transition">
          <p class="text-3xl font-bold text-indigo-300">20+</p>
          <p class="text-gray-300 mt-2">APIs built (secure + scalable)</p>
        </div>

        <div class="rounded-2xl border border-white/10 bg-white/5 p-5 hover:bg-white/10 transition">
          <p class="text-3xl font-bold text-indigo-300">LLM</p>
          <p class="text-gray-300 mt-2">RAG + knowledge graph experience</p>
        </div>

        <div class="rounded-2xl border border-white/10 bg-white/5 p-5 hover:bg-white/10 transition">
          <p class="text-3xl font-bold text-indigo-300">Vue</p>
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

let observer

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

    observer?.disconnect()
    return () => ctx.revert()
  }

  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting) animateIn()
    },
    { threshold: 0.2 }
  )

  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => {
  observer?.disconnect()
})
</script>
