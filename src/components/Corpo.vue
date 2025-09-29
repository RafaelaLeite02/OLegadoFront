<template>
  <main class="flex items-center w-auto bg-stone-950 flex-col p-8 pt-25 min-h-screen">
    <h1 class="text-neutral-50 text-[50px]">
      Os <strong class="text-red-600 font-normal">Imortais</strong>
    </h1>
    <p class="text-neutral-50 text-[20px] m-5">
      Cada personagem carrega consigo séculos de história, poder e mistério. 
      Explore suas origens, habilidades e os laços que os unem nesta saga eterna.
    </p>

    <!-- Filtros -->
    <section
      class="w-[105%] flex flex-col item-center text-center p-5 pt-17 bg-gradient-to-b from-stone-950 via-gray-900 to-stone-950"
    >
      <div
        class="w-[19%] ml-[40%] h-15 flex flex-row justify-between text-center item-center rounded-full text-neutral-50 p-2"
      >
        <a href="#" class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Todos</a>
        <a href="#" class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Livros</a>
        <a href="#" class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Filme</a>
      </div>
      <p class="text-neutral-50 m-5">
        <strong class="text-red-600 font-normal">{{ personagens.length }}</strong> personagens
      </p>
    </section>

    <!-- Cards -->
    <section class="flex flex-wrap m-6 items-center w-[95%] ml-30">
      <Card 
        v-for="personagem in personagens" 
        :key="personagem.Id" 
        :personagem="personagem"
        @abrir="abrirModalComPersonagem" 
        @editar="iniciarEdicao"
        @deletar="deletarPersonagem"
      />
    </section>

    <!-- Modal detalhes -->
    <Modal
      v-if="modalDetalhesVisivel"
      :personagem="personagemSelecionado"
      @fechar="fecharModal"
      @deletar="deletarPersonagem"
      @editar="iniciarEdicao"
    />

    <!-- Modal criar/editar -->
    <CriarPersonagem 
      v-if="modalCriarPersonagemVisivel"
      :personagem="personagemSendoEditado"
      @close="fecharModalCriar"
      @personagem-criado="recarregarPersonagensEFechar"
      @personagem-editado="recarregarPersonagensEFechar"
    />

    <!-- Botão adicionar -->
    <button 
      @click="abrirModalCriar"
      class="mt-6 px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700 transition"
    >
      Adicionar Personagem
    </button>
  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Card from "./Card.vue"; 
import CriarPersonagem from "./CriarPersonagem.vue";
import Modal from "./Modal.vue";
import api from "../services/api";

const personagens = ref([]);
const personagemSelecionado = ref(null); // Usado para o Modal de Detalhes
const personagemSendoEditado = ref(null); // Usado para o Modal de Criação/Edição
const modalDetalhesVisivel = ref(false); // Renomeado para maior clareza
const modalCriarPersonagemVisivel = ref(false);

// ----------------------------------------------------------------------
// ## API
// ----------------------------------------------------------------------

// Função Principal: Carrega todos os Cards (GET /Personagem)
async function carregarPersonagens() {
  try {
    const response = await api.get("/Personagem");
    personagens.value = response.data;
  } catch (error) {
    console.error("Erro ao carregar dados da API:", error);
  }
}

// NOVO: Função para buscar o Personagem por ID (GET /Personagem/{id})
// Essencial para o Modal de Detalhes.
async function buscarDetalhesPersonagem(id) {
  try {
    const response = await api.get(`/Personagem/${id}`);
    return response.data;
  } catch (error) {
    console.error(`Erro ao buscar detalhes do personagem ${id}:`, error);
    return null;
  }
}

const deletarPersonagem = async (personagemParaDeletar) => {
  try {
    // É uma boa prática pedir confirmação aqui
    if (confirm(`Tem certeza que deseja deletar ${personagemParaDeletar.Nome}?`)) {
      await api.delete(`/Personagem/${personagemParaDeletar.id}`); // Assumindo que o ID é 'id' (minúsculo) no backend C#
      await carregarPersonagens(); // Recarrega a lista
      fecharModalDetalhes(); // Fecha o modal após deletar
    }
  } catch (error) {
    console.error("Erro ao deletar personagem:", error);
  }
};

// ----------------------------------------------------------------------
// ## MODAIS - DETALHES
// ----------------------------------------------------------------------

// ATUALIZADO: Busca os detalhes mais recentes antes de abrir o modal
const abrirModalComPersonagem = async (personagem) => {
  const detalhes = await buscarDetalhesPersonagem(personagem.id);
  if (detalhes) {
    personagemSelecionado.value = detalhes;
    modalDetalhesVisivel.value = true;
  }
};

const fecharModalDetalhes = () => {
  personagemSelecionado.value = null;
  modalDetalhesVisivel.value = false;
};

// ----------------------------------------------------------------------
// ## MODAIS - CRIAÇÃO/EDIÇÃO
// ----------------------------------------------------------------------

// ATUALIZADO: Chamado quando o Modal de Criação/Edição fecha (e salva)
const recarregarPersonagensEFechar = async () => {
  await carregarPersonagens();
  fecharModalCriar();
};

const abrirModalCriar = () => {
  personagemSendoEditado.value = null; // Garante que está em modo de criação
  modalCriarPersonagemVisivel.value = true;
};

// ATUALIZADO: Busca os detalhes mais recentes do personagem para pré-preencher o formulário
const iniciarEdicao = async (personagemDoCard) => {
  const detalhesCompletos = await buscarDetalhesPersonagem(personagemDoCard.id);
  
  if (detalhesCompletos) {
    personagemSendoEditado.value = detalhesCompletos;
    modalCriarPersonagemVisivel.value = true;
    fecharModalDetalhes(); // Fecha o Modal de Detalhes se estiver aberto
  }
};

const fecharModalCriar = () => {
  modalCriarPersonagemVisivel.value = false;
  personagemSendoEditado.value = null;
};

// ----------------------------------------------------------------------
// ## LIFECYCLE
// ----------------------------------------------------------------------

onMounted(() => {
  carregarPersonagens();
});
</script>
