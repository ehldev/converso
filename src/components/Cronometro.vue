<template>
  <div class="stopwatch absolute bottom-0 right-0">
    <h2>Cronómetro</h2>
    <p class="time">{{ formattedTime }}</p>
    <div class="controls">
      <button @click="start" :disabled="isRunning">Iniciar</button>
      <button @click="pause" :disabled="!isRunning">Pausar</button>
      <button @click="reset">Reiniciar</button>
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

<style scoped>
.stopwatch {
  text-align: center;
  font-family: Arial, sans-serif;
}
.time {
  font-size: 2rem;
  margin: 10px 0;
}
.controls button {
  margin: 0 5px;
  padding: 6px 12px;
  border: none;
  background: #365EFF;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}
.controls button:disabled {
  background: #999;
  cursor: not-allowed;
}
</style>