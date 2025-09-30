<template>
    <div class="fixed inset-0 z-50 flex items-center justify-center bg-gradient-to-b from-stone-950  via-red-950 to-stone-950 bg-opacity-75 ">
        <div class="w-full max-w-5xl overflow-y-auto max-h-[90vh] rounded-xl bg-gradient-to-b from-stone-950 via-red-950 to-stone-950 bg-opacity-75 shadow-2xl">
            <div class="relative p-8">
                <button @click="$emit('fechar')" class="absolute right-6 top-6 text-gray-400 hover:text-white transition-colors duration-200">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>

                <div class="absolute top-6 left-6 flex space-x-2">
                    <button @click="$emit('editar', personagem)" class="p-2 rounded-full text-white bg-blue-900 hover:bg-blue-600 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" />
                            <path fill-rule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clip-rule="evenodd" />
                        </svg>
                    </button>
                    <button @click="$emit('deletar', personagem)" class="p-2 rounded-full text-white bg-red-900 hover:bg-red-700 transition">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                        </svg>
                    </button>
                </div>

                <div class="flex flex-col items-center p-6 text-center">
                    <div class="relative mb-6">
                        <img class="h-64 w-64 rounded-full border-4 border-red-700 object-cover shadow-lg" :src="personagem.fotoURL" :alt="personagem.name" />
                        <div class="absolute bottom-2 right-2 flex items-center gap-1 rounded-full bg-red-700 px-3 py-1 text-xs font-semibold text-white">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
                                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                            </svg>
                            {{ personagem.tipoCriatura }}
                        </div>
                    </div>
                    <h1 class="text-5xl font-bold text-white">{{ personagem.name }}</h1>
                    <p class="mt-1 text-lg text-gray-400">{{ personagem.tipoCriatura }}</p>
                </div>
                
                <div class="flex flex-col md:flex-row p-6">
                    <div class="flex-1 space-y-8 md:border-r md:border-gray-800 md:pr-8">
                        <div>
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300">História & Biografia</h2>
                            <p class="text-gray-300 leading-relaxed bg-gray-800 items-center rounded-lg p-3 mt-3">
                                {{ personagem.descricao }}
                            </p>
                        </div>
                         <div class="flex flex-row justify-between">
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300 w-[48%] ">Idade
                              <p class="text-gray-300 leading-relaxed text-base font-normal items-center gap-3 rounded-lg bg-gray-800 p-3 mt-3">
                                {{ personagem.idade }}
                            </p></h2>
                            
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300 w-[48%]">Cla
                              <p class="text-gray-300 leading-relaxed text-base font-normal items-center gap-3 rounded-lg bg-gray-800 p-3 mt-3">
                                {{ personagem.cla }}
                            </p></h2>
                            
                        </div>
                        <div v-if="personagem.habilidades">
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300">Habilidades & Poderes</h2>
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div class="flex items-center gap-3 rounded-lg bg-gray-800 p-3" v-for="habilidade in personagem.habilidades" :key="habilidade">
                                    <span class="h-3 w-3 rounded-full bg-red-600"></span>
                                    <span class="text-sm font-semibold text-gray-200">{{ habilidade }}</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="md:w-1/3 md:pl-8 mt-8 md:mt-0 space-y-8">
                        <div v-if="personagem.personalidade">
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300">Personalidade</h2>
                            <ul class="space-y-3">
                                <li class="flex items-center gap-2 text-gray-300" v-for="caracteristica in personagem.personalidade" :key="caracteristica">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-600" viewBox="0 0 20 20" fill="currentColor">
                                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                                    </svg>
                                    {{ caracteristica }}
                                </li>
                            </ul>
                        </div>
                        <div v-if="personagem.nivelPoder">
                            <h2 class="mb-3 text-2xl font-bold text-neutral-300">Estatísticas</h2>
                            <div class="flex flex-col items-center">
                                <span class="text-6xl font-bold text-red-600">{{ personagem.nivelPoder }}</span>
                                <span class="text-lg text-gray-400">Nível de Poder</span>
                                <div class="mt-4 h-2 w-full rounded-full bg-gray-800">
                                    <div class="h-2 rounded-full bg-red-600" :style="{ width: (personagem.nivelPoder * 10) + '%' }"></div>
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
    personagem: {
        type: Object,
        default: null
    }
});


const emit = defineEmits(['fechar', 'editar', 'deletar']);
</script>