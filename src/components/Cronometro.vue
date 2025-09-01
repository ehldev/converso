<template>
  <div
    class="stopwatch absolute bottom-6 right-6 select-none"
    aria-label="Cronómetro"
  >
    <div
      class="flex items-center gap-4 bg-white/80 dark:bg-slate-900/80 backdrop-blur-md border border-slate-200/60 dark:border-slate-700/60 shadow-lg rounded-2xl pl-4 pr-3 py-3"
    >
      <!-- Etiqueta -->
      <span class="text-xs font-semibold tracking-wide text-slate-600 dark:text-slate-300 uppercase">
        Cronómetro
      </span>

      <!-- Tiempo -->
      <span
        class="text-3xl font-mono tabular-nums font-bold text-slate-900 dark:text-white tracking-tight px-3 py-1 rounded-lg bg-slate-100/80 dark:bg-slate-800/70 border border-slate-200 dark:border-slate-700"
      >
        {{ formattedTime }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Stopwatch",
  data() {
    return {
      time: 0,         // tiempo en segundos
      timer: null,     // referencia al setInterval
      isRunning: false
    }
  },
  mounted() {
    this.start()
  },
  computed: {
    formattedTime() {
      const hours = Math.floor(this.time / 3600).toString().padStart(2, "0")
      const minutes = Math.floor((this.time % 3600) / 60).toString().padStart(2, "0")
      const seconds = (this.time % 60).toString().padStart(2, "0")
      return `${hours}:${minutes}:${seconds}`
    }
  },
  methods: {
    start() {
      if (!this.isRunning) {
        this.isRunning = true
        this.timer = setInterval(() => {
          this.time++
        }, 1000)
      }
    },
    pause() {
      this.isRunning = false
      clearInterval(this.timer)
      this.timer = null
    },
    reset() {
      this.pause()
      this.time = 0
    }
  },
  beforeDestroy() {
    if (this.timer) clearInterval(this.timer)
  }
}
</script>

<!-- Sin estilos CSS adicionales: todo con clases Tailwind -->