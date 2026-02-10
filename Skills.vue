<template>
  <section id="skills" class="bg-gray-950 text-white px-6 py-24">
    <div class="max-w-6xl mx-auto">
      <div class="flex items-end justify-between gap-6 flex-wrap">
        <div>
          <h2 class="text-3xl md:text-4xl font-bold">Skills</h2>
          <p class="text-gray-300 mt-3 max-w-2xl">
            Click a category to filter. This is built with Vue state + transitions.
          </p>
        </div>
      </div>

      <!-- Filter chips -->
      <div class="mt-8 flex flex-wrap gap-2">
        <button
          v-for="c in categories"
          :key="c"
          class="px-4 py-2 rounded-full text-sm border border-white/10 transition
                 hover:bg-white/10"
          :class="active === c ? 'bg-indigo-600 border-indigo-500 text-white' : 'bg-white/5 text-gray-200'"
          @click="active = c"
        >
          {{ c }}
        </button>
      </div>

      <!-- Animated grid -->
      <TransitionGroup
        name="fade"
        tag="div"
        class="mt-10 grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-3"
      >
        <div
          v-for="s in filtered"
          :key="s.name"
          class="rounded-2xl border border-white/10 bg-white/5 px-4 py-4
                 hover:bg-white/10 transition hover:-translate-y-0.5"
        >
          <p class="font-medium text-white">{{ s.name }}</p>
          <p class="text-xs text-gray-400 mt-1">{{ s.level }}</p>
        </div>
      </TransitionGroup>
    </div>
  </section>
</template>

<script setup>
import { computed, ref } from "vue"

const categories = ["All", "Frontend", "Backend", "Python/AI", "Cloud/DevOps"]

const active = ref("All")

const skills = [
  { name: "Vue 3", level: "Advanced", cat: "Frontend" },
  { name: "JavaScript", level: "Advanced", cat: "Frontend" },
  { name: "Tailwind CSS", level: "Advanced", cat: "Frontend" },
  { name: "Node.js", level: "Intermediate", cat: "Backend" },
  { name: "REST APIs", level: "Advanced", cat: "Backend" },
  { name: "Python", level: "Advanced", cat: "Python/AI" },
  { name: "FastAPI", level: "Intermediate", cat: "Python/AI" },
  { name: "RAG / LLM Apps", level: "Intermediate", cat: "Python/AI" },
  { name: "PostgreSQL", level: "Intermediate", cat: "Backend" },
  { name: "Docker", level: "Intermediate", cat: "Cloud/DevOps" },
  { name: "AWS", level: "Intermediate", cat: "Cloud/DevOps" },
  { name: "GitHub Actions", level: "Intermediate", cat: "Cloud/DevOps" },
]

const filtered = computed(() => {
  if (active.value === "All") return skills
  return skills.filter((s) => s.cat === active.value)
})
</script>

<style scoped>
/* Vue transition group */
.fade-enter-active,
.fade-leave-active {
  transition: all 220ms ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(8px);
}
</style>
