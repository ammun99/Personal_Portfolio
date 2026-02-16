<template>
  <section id="contact" class="bg-gray-950 text-white px-6 py-24">
    <div class="max-w-6xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-10 items-start">
      <div>
        <h2 class="text-3xl md:text-4xl font-bold">Contact</h2>
        <p class="text-gray-300 mt-3 max-w-xl">
          Let's connect, Send a message. (Next step: wire this to a Python FastAPI endpoint.)
        </p>

        <div class="mt-8 space-y-3 text-sm text-gray-300">
          <p>
            <span class="text-gray-400">Email:</span>
            <a class="text-indigo-300 hover:text-indigo-200 transition" href="mailto:amruthanagaraj99@gmail.com">
              amruthanagaraj41@gmail.com
            </a>
          </p>
          <p>
            <span class="text-gray-400">GitHub:</span>
            <a class="text-indigo-300 hover:text-indigo-200 transition" href="https://github.com/ammun99" target="_blank" rel="noreferrer">
              github.com/ammun99
            </a>
          </p>
          <p>
            <span class="text-gray-400">LinkedIn:</span>
            <a class="text-indigo-300 hover:text-indigo-200 transition" href="https://linkedin.com/in/amrutha-nagaraj-0158881a1/" target="_blank" rel="noreferrer">
              linkedin.com/in/amrutha-nagaraj-0158881a1/
            </a>
          </p>
        </div>
      </div>

      <form
        class="rounded-2xl border border-white/10 bg-white/5 p-6 space-y-4"
        @submit.prevent="submit"
      >
        <div>
          <label class="text-sm text-gray-300">Name</label>
          <input
            v-model="name"
            type="text"
            required
            class="mt-2 w-full rounded-xl bg-black/30 border border-white/10 px-4 py-3
                   outline-none focus:ring-2 focus:ring-indigo-500/60 focus:border-indigo-400/40 transition"
            placeholder="Your name"
          />
        </div>

        <div>
          <label class="text-sm text-gray-300">Email</label>
          <input
            v-model="email"
            type="email"
            required
            class="mt-2 w-full rounded-xl bg-black/30 border border-white/10 px-4 py-3
                   outline-none focus:ring-2 focus:ring-indigo-500/60 focus:border-indigo-400/40 transition"
            placeholder="you@example.com"
          />
        </div>

        <div>
          <label class="text-sm text-gray-300">Message</label>
          <textarea
            v-model="message"
            rows="5"
            required
            class="mt-2 w-full rounded-xl bg-black/30 border border-white/10 px-4 py-3
                   outline-none focus:ring-2 focus:ring-indigo-500/60 focus:border-indigo-400/40 transition"
            placeholder="Tell me what you want to build..."
          ></textarea>
        </div>

        <button
          type="submit"
          class="w-full rounded-xl bg-indigo-600 hover:bg-indigo-500 transition
                 py-3 font-medium hover:-translate-y-0.5 transform duration-200"
          :disabled="sending"
        >
          <span v-if="!sending && !sent">Send Message</span>
          <span v-else-if="sending">Sending...</span>
          <span v-else>Sent ✓</span>
        </button>

        <p v-if="sent" class="text-sm text-green-300 text-center">
          Message sent!.
        </p>
      </form>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue"
import emailjs from "@emailjs/browser"

const name = ref("")
const email = ref("")
const message = ref("")

const sending = ref(false)
const sent = ref(false)

async function submit() {
  sent.value = false
  sending.value = true

  try {
    await emailjs.send(
      "service_kgmkern", // ✅ Your Service ID
      "template_nqolwbi", // ⭐ Replace this
      {
        from_name: name.value,
        reply_to: email.value,
        message: message.value,
      },
      "XaPmWGmwoTaPU1noF" // ⭐ Replace this
    )

    sent.value = true

    // Reset form
    name.value = ""
    email.value = ""
    message.value = ""
  } catch (err) {
    console.error("EmailJS error:", err)
    alert("Message failed to send. Please try again.")
  } finally {
    sending.value = false
  }
}
</script>
