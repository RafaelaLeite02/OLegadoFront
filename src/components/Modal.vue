<template>
  <div v-if="visivel" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-75">
    <div class="w-full max-w-5xl overflow-y-auto rounded-xl bg-gray-950 shadow-2xl">
      <div class="relative p-8">
        <button @click="$emit('fechar')" class="absolute right-6 top-6 text-gray-400 hover:text-white transition-colors duration-200">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>

        <div class="flex flex-col items-center p-6 text-center">
            <div class="relative mb-6">
              <img class="h-64 w-64 rounded-full border-4 border-red-500 object-cover shadow-lg" src="https://via.placeholder.com/256/111827/F3F4F6" alt="Edward Anthony Cullen" />
              <div class="absolute bottom-2 right-2 flex items-center gap-1 rounded-full bg-red-500 px-3 py-1 text-xs font-semibold text-white">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                </svg>
                Vampiro
              </div>
            </div>
            <h1 class="text-5xl font-bold text-white">Edward Anthony Cullen</h1>
            <p class="mt-1 text-lg text-gray-400">O Leitor de Mentes</p>
          </div>
          <div class="flex flex-col md:flex-row p-6">
            <div class="flex-1 space-y-8 md:border-r md:border-gray-800 md:pr-8">
              <div>
                <h2 class="mb-3 text-2xl font-bold text-red-500">História & Biografia</h2>
                <p class="text-gray-300 leading-relaxed">
                  Edward Anthony Masen nasceu em 1901 em Chicago e foi transformado em vampiro por Carlisle Cullen em 1918, durante a pandemia de gripe espanhola.
                  Possui a habilidade rara de ler mentes, conseguindo ouvir os pensamentos de qualquer pessoa, exceto Bella Swan. Membro dedicado da família Cullen,
                  segue rigorosamente a dieta 'vegetariana' de sangue animal.
                </p>
              </div>
              <div>
                <h2 class="mb-3 text-2xl font-bold text-red-500">Habilidades & Poderes</h2>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div class="flex items-center gap-3 rounded-lg bg-gray-800 p-3">
                    <span class="h-3 w-3 rounded-full bg-red-500"></span>
                    <span class="text-sm font-semibold text-gray-200">Leitura Mental</span>
                  </div>
                  <div class="flex items-center gap-3 rounded-lg bg-gray-800 p-3">
                    <span class="h-3 w-3 rounded-full bg-red-500"></span>
                    <span class="text-sm font-semibold text-gray-200">Velocidade Sobre-humana</span>
                  </div>
                  <div class="flex items-center gap-3 rounded-lg bg-gray-800 p-3">
                    <span class="h-3 w-3 rounded-full bg-red-500"></span>
                    <span class="text-sm font-semibold text-gray-200">Força Vampírica</span>
                  </div>
                  <div class="flex items-center gap-3 rounded-lg bg-gray-800 p-3">
                    <span class="h-3 w-3 rounded-full bg-red-500"></span>
                    <span class="text-sm font-semibold text-gray-200">Composição Musical</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="md:w-1/3 md:pl-8 mt-8 md:mt-0 space-y-8">
              <div>
                <h2 class="mb-3 text-2xl font-bold text-red-500">Personalidade</h2>
                <ul class="space-y-3">
                  <li class="flex items-center gap-2 text-gray-300">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-500" viewBox="0 0 20 20" fill="currentColor">
                      <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                    </svg>
                    Protetor
                  </li>
                  <li class="flex items-center gap-2 text-gray-300">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-500" viewBox="0 0 20 20" fill="currentColor">
                      <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                    </svg>
                    Melancólico
                  </li>
                </ul>
              </div>
              <div>
                <h2 class="mb-3 text-2xl font-bold text-red-500">Estatísticas</h2>
                <div class="flex flex-col items-center">
                  <span class="text-6xl font-bold text-white">9</span>
                  <span class="text-lg text-gray-400">Nível de Poder</span>
                  <div class="mt-4 h-2 w-full rounded-full bg-gray-800">
                    <div class="h-2 w-[90%] rounded-full bg-red-500"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script setup>

import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  visivel: {
    type: Boolean,
    default: false,
  },
});


const emit = defineEmits(['fechar']);
</script>