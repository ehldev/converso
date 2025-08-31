<!-- WelcomeScreen.vue — Vue 2 + Tailwind (espaciado fiel a la referencia) -->
<template>
  <div class="bg-white min-h-screen flex flex-col justify-center items-center">

    <img src="@/assets/images/layout/logo.png" alt="Converso - Apoyo emocional instantáneo" class="w-60 mx-auto">


    <!-- ILUSTRACIÓN -->
    <div class="pt-10 px-6">
      <img
        src="@/assets/images/welcome/slide-1.png"
        alt="Welcome"
        class="w-[85%] max-w-[300px] select-none pointer-events-none mx-auto"
        draggable="false"
      />
    </div>

    <!-- COPY + DOTS (bloque compacto) -->
    <section class="mt-4 px-8 text-center">
      <h1 class="max-w-[90%] mx-auto text-[24px] font-bold text-slate-900">
        El mejor momento para hablar es ahora
      </h1>
      <p class="mt-2 text-slate-600 text-[14px] leading-relaxed max-w-[300px] mx-auto">
        Habla al instante con <b>Converso</b> y encuentra apoyo cuando más lo necesitas.
      </p>

      <div class="flex items-center justify-center gap-2 mt-6">
        <span class="h-1.5 w-1.5 rounded-full bg-slate-300"></span>
        <span class="h-1.5 w-5 rounded-full" :style="{ backgroundColor: primary }"></span>
        <span class="h-1.5 w-1.5 rounded-full bg-slate-300"></span>
        <span class="h-1.5 w-1.5 rounded-full bg-slate-300"></span>
      </div>
    </section>

    <!-- BOTÓN (cerca del contenido, no pegado al borde) -->
    <div class="w-full text-center px-8 mt-12 mb-8">
      <router-link to="/about"
        class="flex justify-center items-center max-w-[220px] h-12 mx-auto uppercase rounded-[14px] text-white font-medium shadow-[0_10px_20px_rgba(16,185,129,.35)] active:scale-[.99] transition"
        :style="{ backgroundColor: primary }"
      >
        Probar ahora
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WelcomeScreen',
  props: {
    title: { type: String, default: 'Choose the suitable class for you' },
    subtitle: {
      type: String,
      default: 'We have expert team & you can book with them your Classes'
    },
    primary: { type: String, default: '#10B981' }, // verde del ejemplo
  }
}
</script>

<style scoped>
/* Limpio: sin ripple/carrusel/card */
</style>
