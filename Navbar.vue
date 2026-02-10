<template>
  <header class="fixed top-0 left-0 right-0 z-50">
    <div class="mx-auto max-w-6xl px-6">
    <div class="h-[2px] w-full bg-white/10">
  <div
    class="h-full bg-indigo-400 transition-[width] duration-150"
    :style="{ width: progress + '%' }"
  ></div>
</div>

      <nav
        class="mt-4 flex items-center justify-between rounded-2xl border border-white/10
               bg-gray-900/60 backdrop-blur-xl px-4 py-3 shadow-lg shadow-black/20"
      >
        <a
          href="#"
          class="font-semibold tracking-tight text-white hover:text-indigo-300 transition"
          @click.prevent="scrollTo('top')"
        >
          Amrutha Nagaraj <span class="text-indigo-400">.</span>
        </a>

<div class="hidden md:flex items-center gap-6 text-sm">
  <button
    v-for="item in items"
    :key="item.id"
    class="relative text-gray-300 hover:text-white transition"
    @click="scrollTo(item.id)"
  >
    <span
      class="absolute -bottom-2 left-0 h-[2px] w-full rounded bg-indigo-400 transition-opacity"
      :class="activeId === item.id ? 'opacity-100' : 'opacity-0'"
    ></span>
    {{ item.label }}
  </button>

  <a
    href="/resume.pdf"
    target="_blank"
    class="px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-500 transition text-white"
  >
    Resume
  </a>
</div>


        <button
          class="md:hidden text-gray-300 hover:text-white transition"
          @click="open = !open"
        >
          ☰
        </button>
      </nav>

      <!-- Mobile menu -->
      <div
        v-if="open"
        class="md:hidden mt-3 rounded-2xl border border-white/10 bg-gray-900/80 backdrop-blur-xl p-3"
      >
        <button
          v-for="item in items"
          :key="item.id"
          class="w-full text-left px-3 py-2 rounded-lg text-gray-200 hover:bg-white/5 transition"
          @click="scrollTo(item.id); open=false"
        >
          {{ item.label }}
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from "vue"

const open = ref(false)
const activeId = ref("")
const progress = ref(0)


const items = [
  { id: "about", label: "About" },
  { id: "projects", label: "Projects" },
  { id: "skills", label: "Skills" },
  { id: "contact", label: "Contact" },
]

function scrollTo(id) {
  if (id === "top") {
    window.scrollTo({ top: 0, behavior: "smooth" })
    return
  }
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: "smooth", block: "start" })
}

function onScroll() {
  // Active section highlight
  const offset = 120
  let current = ""
  for (const item of items) {
    const el = document.getElementById(item.id)
    if (!el) continue
    const top = el.getBoundingClientRect().top
    if (top - offset <= 0) current = item.id
  }
  activeId.value = current

  // Scroll progress
  const scrollTop = window.scrollY
  const docHeight = document.documentElement.scrollHeight - window.innerHeight
  const pct = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0
  progress.value = Math.max(0, Math.min(100, pct))
}


onMounted(() => {
  window.addEventListener("scroll", onScroll, { passive: true })
  onScroll()
})

onBeforeUnmount(() => {
  window.removeEventListener("scroll", onScroll)
})
</script>
