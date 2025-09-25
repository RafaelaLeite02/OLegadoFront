<template>
  <div class="p-8">
   

    <div class="flex justify-center">
      <CharacterCard @abrir-modal="mostrarModal = true" />
    </div>

    <Modal :visivel="mostrarModal" @fechar="mostrarModal = false" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import CharacterCard from './CharacterCard.vue';
import Modal from './Modal.vue';

const mostrarModal = ref(false);
</script>