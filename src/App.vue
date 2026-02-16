<template>
  <div class="relative overflow-x-hidden">
    <!-- Cursor Glow -->
    <div ref="cursorGlow" class="cursor-glow"></div>

    <!-- App Content -->
    <Navbar />
    <main>
      <Hero />
      <Sections />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue"
import { gsap } from "gsap"

import Navbar from "./components/Navbar.vue"
import Hero from "./components/Hero.vue"
import Sections from "./components/Sections.vue"

const cursorGlow = ref(null)

onMounted(() => {
  window.addEventListener("mousemove", (e) => {
    gsap.to(cursorGlow.value, {
      x: e.clientX - 200,
      y: e.clientY - 200,
      duration: 0.4,
      ease: "power3.out",
    })
  })
})
</script>

<style>
.cursor-glow {
  position: fixed;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  pointer-events: none;
  background: radial-gradient(circle, rgba(99,102,241,0.25), transparent 60%);
  filter: blur(80px);
  z-index: 0;
}
</style>
