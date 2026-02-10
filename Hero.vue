<template>

  <section class="min-h-screen pt-28 bg-gray-950 text-white relative overflow-hidden">

  <!-- Background video -->
<!-- VIDEO DEBUG (temporary) -->
<video
  class="absolute inset-0 w-full h-full object-cover opacity-100 blur-0"
  autoplay
  muted
  loop
  playsinline
  controls
>
  <source :src="heroVideo" type="video/mp4" />
</video>

<!-- remove overlay for debug -->
<!-- <div class="absolute inset-0 bg-black/70"></div> -->



    <!-- Subtle background glow blobs -->
    <div class="absolute inset-0 opacity-40 pointer-events-none">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
    </div>

    <div class="relative z-10 max-w-6xl mx-auto px-6 py-20 flex flex-col justify-center min-h-screen">

      <div class="space-y-6">
        <p ref="kicker" class="text-sm tracking-widest text-gray-400 uppercase">
          Vue • JavaScript • Python
        </p>

        <h1 ref="title" class="text-5xl md:text-6xl font-bold leading-tight">
          Hi, I’m <span class="text-indigo-400">Amrutha</span> 👋
          <br />
          I'm a Full-Stack and Software Engineer.
        </h1>

        <p ref="subtitle" class="text-lg md:text-xl text-gray-300 max-w-2xl">
          I create interactive, animated, responsive websites using Vue.js and Tailwind CSS —
          and connect them to scalable Python backends, and  with hands-on experience in building scalable web applications, backend services, cloud-native systems, and data pipelines using Java, TypeScript, Node.js, React, and AWS. Seeking to contribute to a growth-driven engineering team by building reliable, high-performance, and maintainable software systems..
        </p>

        <div ref="ctaRow" class="flex flex-wrap gap-4 pt-4">
<button
  class="px-6 py-3 rounded-xl bg-indigo-600 hover:bg-indigo-500 transition
         shadow-lg shadow-indigo-600/20 hover:shadow-indigo-500/30
         hover:-translate-y-0.5 transform duration-200"
  @click="scrollTo('projects')"
>
  View My Projects
</button>

<button
  class="px-6 py-3 rounded-xl border border-gray-700 hover:border-gray-500 transition
         bg-white/0 hover:bg-white/5
         hover:-translate-y-0.5 transform duration-200"
  @click="scrollTo('contact')"
>
  Contact Me
</button>

        </div>

        <div ref="chips" class="flex flex-wrap gap-2 pt-8">
          <span class="chip">Vue 3</span>
          <span class="chip">Tailwind</span>
          <span class="chip">GSAP</span>
          <span class="chip">FastAPI</span>
          <span class="chip">PostgreSQL</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import heroVideo from "../assets/hero-bg.mp4"
import { ref, onMounted } from "vue"
import { gsap } from "gsap"

const kicker = ref(null)
const title = ref(null)
const subtitle = ref(null)
const ctaRow = ref(null)
const chips = ref(null)
function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" })
}


onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: "power3.out" } })

  tl.from(kicker.value, { opacity: 0, y: 12, duration: 0.5 })
    .from(title.value, { opacity: 0, y: 18, duration: 0.7 }, "-=0.2")
    .from(subtitle.value, { opacity: 0, y: 14, duration: 0.6 }, "-=0.35")
    .from(ctaRow.value, { opacity: 0, y: 10, duration: 0.5 }, "-=0.35")
    .from(chips.value, { opacity: 0, y: 10, duration: 0.5 }, "-=0.3")
})
</script>

<style scoped>
/* chip style (uses Tailwind via @apply) */
.chip {
  @apply text-sm px-3 py-1 rounded-full border border-gray-700 text-gray-300 bg-white/5;
}

/* Soft glow blobs */
.blob {
  position: absolute;
  width: 520px;
  height: 520px;
  filter: blur(60px);
  border-radius: 9999px;
  background: radial-gradient(circle at 30% 30%, rgba(99, 102, 241, 0.6), rgba(0, 0, 0, 0));
}
.blob-1 {
  top: -160px;
  left: -120px;
}
.blob-2 {
  bottom: -180px;
  right: -140px;
  background: radial-gradient(circle at 30% 30%, rgba(236, 72, 153, 0.55), rgba(0, 0, 0, 0));
}
</style>
