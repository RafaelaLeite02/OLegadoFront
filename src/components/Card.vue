<template>
  <section class="relative w-100 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10 ">
    <div class="relative h-55">
      <img :src="getImageSrc(personagem.fotoURL)" :alt="personagem.name" class="w-full h-full object-cover"
        @error="personagem.fotoURL = 'https://via.placeholder.com/300'" />

      <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

      <span class="absolute top-2 right-2 bg-red-600 text-white px-2 py-1 rounded-full text-xs">
        {{ personagem.tipoCriatura || 'N/A' }}
      </span>

      <div class="absolute bottom-3 left-3">
        <h2 class="text-xl font-bold">{{ personagem.name }}</h2>
      </div>
    </div>

    <div class="p-5 space-y-4">
      <p class="text-sm text-gray-300">
        {{ personagem.descricao }}
      </p>

      <div>
        <p class="text-xs uppercase text-gray-400">Idade:</p>
        <p class="text-sm font-medium">{{ personagem.idade }}</p>
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

const getImageSrc = (fotoURL) => {
  if (!fotoURL) return "https://via.placeholder.com/300";

  // Se começar com "http" → é uma URL normal
  if (fotoURL.startsWith("http")) {
    return fotoURL;
  }

  // Se for base64 puro → monta corretamente
  return `data:image/png;base64,${fotoURL}`;
};

const emit = defineEmits(['abrir-modal']);
</script>