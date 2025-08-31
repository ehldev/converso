<template>
  <div class="h-[100vh] animate__animated animate__fadeIn"
    :class="{ 'bg-gradient-to-br from-[rgba(53,73,94,0.8)] to-[rgba(0,191,166,0.8)]': !isReady }">
    <!-- Header -->
    <header class="px-4 py-3 flex items-center justify-between bg-secondary" v-if="isReady">
      <div class="flex items-center gap-2">
        <!-- Logo -->
        <router-link to="/">
          <img src="@/assets/images/layout/logo-blanco.png" alt="Converso - Apoyo emocional instantáneo"
            class="w-32"></img>
        </router-link>
      </div>
      <button class="text-sm px-3 py-1 rounded-lg bg-red-500 text-white">
        Salir
        <i class="ri-logout-box-r-line"></i>
      </button>
    </header>

    <!-- Recomendaciones previas -->
    <div class="animate__animated animate__fadeInRight flex flex-column justify-center items-center"
      :class="isReady ? 'h-[calc(100vh-100px)]' : 'h-full'">
      <section v-if="!isReady" class="max-w-5xl mx-auto pt-12 pb-16 px-6 lg:px-10">
        <img src="@/assets/images/layout/logo-blanco.png" alt="Converso - Apoyo emocional instantáneo"
          class="w-60 mx-auto">

        <div class="text-center my-6">
          <h1 class="text-4xl text-white font-bold mb-4">¡Prepárate para tu sesión!</h1>
          <p class="text-lg text-white/80">
            Sigue estas recomendaciones para sacar el máximo provecho de tu conversación.
          </p>
        </div>

        <div class="grid md:grid-cols-2 gap-10 items-start mt-10">
          <!-- Tips izq -->
          <div class="space-y-6">
            <div class="bg-secondary/10 rounded-2xl p-5 flex items-start gap-4 shadow-md">
              <i class="ri-mic-line text-3xl text-primary font-bold"></i>
              <div>
                <h3 class="text-xl text-white font-bold">Habla con claridad</h3>
                <p class="text-sm text-white/70">
                  Imagina que estás en una videollamada real. Evita hablar muy rápido.
                </p>
              </div>
            </div>
            <div class="bg-secondary/10 rounded-2xl p-5 flex items-start gap-4 shadow-md">
              <i class="ri-user-heart-line text-3xl text-primary font-bold"></i>
              <div>
                <h3 class="text-xl text-white font-bold">Mantén la calma</h3>
                <p class="text-sm text-white/70">
                  No pasa nada si te equivocas. Esta sesión es para practicar y mejorar.
                </p>
              </div>
            </div>
          </div>
          <!-- Tips der -->
          <div class="space-y-6">
            <div class="bg-secondary/10 rounded-2xl p-5 flex items-start gap-4 shadow-md">
              <i class="ri-lightbulb-flash-line text-3xl text-primary font-bold"></i>
              <div>
                <h3 class="text-xl text-white font-bold">Sé creativo</h3>
                <p class="text-sm text-white/70">
                  No memorices respuestas. Responde como lo harías de forma natural.
                </p>
              </div>
            </div>
            <!-- <div class="bg-secondary/10 rounded-2xl p-5 flex items-start gap-4 shadow-md">
            <i class="ri-time-line text-3xl text-secondary font-bold"></i>
            <div>
              <h3 class="text-xl text-white font-semibold">Aprovecha el tiempo</h3>
              <p class="text-sm text-white/70">
                La conversación es corta. Mantén el enfoque en tu objetivo.
              </p>
            </div>
          </div> -->
          </div>
        </div>

        <!-- Botón continuar -->
        <div class="mt-12 md:mt-8" @click="isReady = true">
          <button
            class="w-full bg-gradient-to-br from-[rgba(53,73,94,0.8)] to-[rgba(0,191,166,0.8)] flex justify-center items-center max-w-[220px] h-12 mx-auto uppercase rounded-[14px] text-white font-medium shadow-[0_10px_20px_rgba(16,185,129,.35)] active:scale-[.99] transition">
            Estoy listo
            <i class="ri-arrow-right-up-line ml-2"></i>
          </button>
        </div>
      </section>

      <!-- Vista de sesión activa -->
      <section v-else class="h-auto w-full flex flex-col items-center justify-center gap-8 pt-10 pb-16">
        <div class="relative w-48 h-48 mx-auto mt-20">
          <!-- Fondo animado -->
          <span class="absolute inset-0 -m-6 rounded-full bg-primary/10 blur-2xl"></span>
          <span class="absolute inset-0 -m-2 rounded-full border border-primary/30 animate-ping"></span>
          <div class="circle-bg absolute inset-0 rounded-full flex justify-center items-center">
          </div>

          <!-- Botones -->
          <div class="absolute bottom-[-20px] left-1/2 -translate-x-1/2 flex gap-4 z-10">
            <!-- Llamar -->
            <button :disabled="connected" @click="startAgent"
              class="w-12 h-12 rounded-full bg-green-500 hover:bg-green-600 text-white flex items-center justify-center shadow-lg disabled:opacity-50">
              <i class="ri-phone-line text-lg"></i>
            </button>

            <!-- Colgar -->
            <button :disabled="!connected" @click="stopAgent"
              class="w-12 h-12 rounded-full bg-red-600 text-white flex items-center justify-center shadow-lg disabled:opacity-50">
              ⏹️
            </button>
          </div>
        </div>

        <p class="mt-4 font-semibold" v-if="connected">Empieza a hablar para empezar la conversación...</p>

        <!-- Sugerencia de respuesta -->
        <!-- <div class="bg-indigo-800/40 border border-white/10 rounded-xl p-6 max-w-xl w-full shadow-md">
          <h3 class="text-lg font-semibold mb-2 flex items-center gap-2">
            <i class="ri-lightbulb-line text-yellow-400"></i> Sugerencia de respuesta
          </h3>
          <p class="text-gray-200 leading-relaxed" v-if="!suggestion">
            Aquí se mostrará una sugerencia para que puedas responder a la IA. Puedes usarla como guía o
            inspiración.
          </p>
          <p class="text-gray-200 leading-relaxed" v-else>
            {{ suggestion }}
          </p>
        </div> -->

        <!-- Error -->
        <p v-if="errorMessage" class="text-red-400">{{ errorMessage }}</p>
      </section>

      <Cronometro v-if="showCronometro" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { RealtimeAgent, RealtimeSession } from '@openai/agents/realtime';

import Cronometro from '@/components/Cronometro.vue';

const errorMessage = ref('');
const suggestion = ref('');
const isReady = ref(false);
const connected = ref(false);
const showCronometro = ref(false);

let mathTutorAgent = new RealtimeAgent({
  name: 'Math Tutor',
  handoffDescription: 'Agente especialista en cuestiones de matemáticas',
  instructions:
    'Siempre debes presentarte como "Matetutor" Proporcionas ayuda con problemas de matemáticas.'
});

let biologyTutorAgent = new RealtimeAgent({
  name: 'Biology Tutor',
  handoffDescription: 'Agente especialista en cuestiones de biología',
  instructions:
    'Siempre debes presentarte como "Biotutor" Proporcionas ayuda con problemas de biología.'
});

// 1. Instanciar el agente
const agent = new RealtimeAgent({
  name: 'Greeter',
  instructions: `ROL Y OBJETIVO
- Eres “Converso”, un acompañante emocional 24/7. Escuchas con atención, ayudas a ordenar ideas y ofreces micro-recomendaciones prácticas.
- No eres profesional de la salud. No diagnosticas ni indicas tratamientos. Comunica límites con calidez.
- Solo brindas acompañamiento emocional: escucha activa, contención, psicoeducación ligera, etc.
- Solo atiendes temas relacionado al bienestar emocional si te piden otros temas debes negarte.

Cierre de responsabilidad
- Cuando corresponda: “Recuerda que soy un acompañante virtual y no reemplazo atención médica. Si estás en riesgo o te sientes en peligro, contacta servicios de emergencia locales.”`,
  // handoffs: [mathTutorAgent, biologyTutorAgent]
});

// 2. Instanciar la sesión de voz
// const session = new RealtimeSession(agent, {
//     model: 'gpt-4o-mini-realtime-preview-2025-06-03'
// });

const session = new RealtimeSession(agent);

// 3. Token efímero de cliente actualizado
const clientToken = 'ek_68b3e39ac9148191ab91bf9bf76c6847';

const getInitialToken = async () => {
  return fetch("https://n8n.app.wize.pe/webhook/get-initial-token", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    }
  })
    .then(response => response.json())
    .then(data => {

      console.log('Data')
      console.log(data)

      if (data.value) {
        return data.value
      }
    });
}

// 4. Callback para cuando el agente termina de responder
const onAgentEnd = async (_runContext, _agentInfo, text) => {

  console.log('_runContext:', _runContext);
  console.log('_agentInfo:', _agentInfo);
  console.log('text:', text);

  if (!text) {
    return;
  }

  try {
    const res = await fetch('https://dytia-n8n.doerfz.easypanel.host/webhook/ba372f09-02b8-41df-9e9f-0617ead8cf7f', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ name: 'Erick', message: text, sessionId: new Date().getTime().toString() })
    });
    const data = await res.json();
    suggestion.value = data.output || '';
  } catch (e) {
    suggestion.value = '';
    console.error('Error al generar sugerencia:', e);
  }
};

// 5. Función para iniciar la sesión y suscribir el listener
const startAgent = async () => {
  errorMessage.value = ''; suggestion.value = '';

  let token = await getInitialToken();

  console.log('Token')
  console.log(token)

  try {
    await session.connect({ apiKey: token, voice: 'Cedar' });
    session.on('agent_end', onAgentEnd);
    connected.value = true;
    showCronometro.value = true;
  } catch (err) {
    errorMessage.value = 'Error al conectar: ' + err.message;
    console.error(err);
  }
};

// 6. Función para detener la sesión y desuscribir el listener
const stopAgent = () => {
  session.off('agent_end', onAgentEnd);
  session.close();
  connected.value = false;
};
</script>

<style>
.circle-bg {
  background-image: url('@/assets/images/call/sound_bg.gif');
  background-size: cover;
  animation: orbeshift 10s ease-in-out infinite alternate;
}

@keyframes orbeshift {
  0% {
    background-position: 0% 0%;
    filter: saturate(1);
  }

  50% {
    background-position: 100% 50%;
    filter: saturate(1.05);
  }

  100% {
    background-position: 50% 100%;
    filter: saturate(1);
  }
}
</style>