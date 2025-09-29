<template>
  <section class="relative w-96 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10">
    <div class="relative h-52">
      <img :src="personagem.FotoURL" :alt="personagem.Name" class="w-full h-full object-cover" /> 
      <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

     <!--<span class="absolute top-2 right-2 bg-red-600 text-white px-2 py-1 rounded-full text-xs">
        {{ personagem.Poder || 'N/A' }}
      </span>--> 

      <div class="absolute bottom-3 left-3">
        <h2 class="text-xl font-bold">{{ personagem.Name }}</h2>
      </div>
    </div>

    <div class="p-5 space-y-4">
      <p class="text-sm text-gray-300">
        {{ personagem.Descricao }}
      </p>

      <div>
        <p class="text-xs uppercase text-gray-400">Idade:</p>
        <p class="text-sm font-medium">{{ personagem.Idade }}</p>
      </div>

      <div class="pt-3">
        <button @click="$emit('abrir-modal', personagem)"
          class="w-full bg-gray-800 border border-gray-600 hover:bg-gray-700 text-sm py-2 rounded-lg transition">
          Ver Perfil
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  personagem: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['abrir-modal']);
</script>