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
      class="w-[105%] flex flex-col item-center text-center p-5 pt-17 bg-gradient-to-b from-stone-950 via-gray-900 to-stone-950">
      <div
        class="w-[19%] ml-[40%] h-15 flex flex-row justify-between text-center item-center rounded-full text-neutral-50 p-2">
        <a @click.prevent="setFiltro('Todos')" :class="{ 'border-red-700 text-red-700': filtroAtivo === 'Todos' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Todos</a>
        <a @click.prevent="setFiltro('Livros')" :class="{ 'border-red-700 text-red-700': filtroAtivo === 'Livros' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Livros</a>
        <a @click.prevent="setFiltro('Filme')" :class="{ 'border-red-700 text-red-700': filtroAtivo === 'Filme' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2 hover:border-red-700 hover:text-red-700 transition">Filme</a>
      </div>
      <p class="text-neutral-50 m-5">
        <strong class="text-red-600 font-normal">{{ personagens.length }}</strong> personagens
      </p>
    </section>

    <!-- Cards -->
    <section class="flex flex-wrap m-6 items-center w-[95%] ml-30">
      <Card v-for="personagem in personagens" :key="personagem.id" :personagem="personagem"
        @abrir-modal="abrirModalComPersonagem" @deletar="deletarPersonagem" />
    </section>

    <!-- Modal detalhes -->
    <Modal v-if="modalDetalhesVisivel" :personagem="personagemSelecionado" @fechar="fecharModalDetalhes"
      @deletar="deletarPersonagem" @editar="iniciarEdicao" />

    <!-- Modal criar/editar -->
    <CriarPersonagem v-if="modalCriarPersonagemVisivel" :personagem="personagemSendoEditado" @close="fecharModalCriar"
      @personagem-criado="recarregarPersonagensEFechar" @personagem-editado="recarregarPersonagensEFechar" />

    <button @click="abrirModalCriar"
      class="text-neutral-300 border-0 bg-gradient-to-r from-stone-950 via-gray-900 to-stone-950 text-xl
               hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200
               duration-300 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)] cursor-pointer"> Adicionar

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
const filtroAtivo = ref('Todos');

// ----------------------------------------------------------------------
// ## API
// ----------------------------------------------------------------------

// Função Principal: Carrega todos os Cards (GET /Personagem)
async function carregarPersonagens(filtro = 'Todos') {
  try {
    const response = await api.get(`/Personagem?filtro=${filtro}`);
    personagens.value = response.data;
    console.log("DADOS RECEBIDOS:", response.data);
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
    if (confirm(`Tem certeza que deseja deletar ${personagemParaDeletar.name}?`)) {
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
const abrirModalComPersonagem = async (personagemDoCard) => {

  // TENTATIVA 1: ID Minúsculo (esperado)
  let idParaBuscar = personagemDoCard.id;

  // TENTATIVA 2: ID Maiúsculo (se o serializer do C# forçá-lo)
  if (!idParaBuscar) {
    idParaBuscar = personagemDoCard.Id;
  }

  // Se o ID ainda for inválido, pare a função
  if (!idParaBuscar) {
    console.error("ID do Personagem é inválido (null/undefined). Não é possível buscar detalhes.");
    alert("Erro: ID do personagem não encontrado.");
    return;
  }

  console.log(`1. INICIANDO BUSCA DE DETALHES PARA ID: ${idParaBuscar}`);

  // 1. Pega os detalhes completos da API (usando o ID que achamos)
  const detalhes = await buscarDetalhesPersonagem(idParaBuscar);

  if (detalhes) {
    console.log("2. DETALHES RECEBIDOS. ABRINDO MODAL.");

    modalCriarPersonagemVisivel.value = false;
    // Atribui os dados e abre o modal
    personagemSelecionado.value = detalhes;
    modalDetalhesVisivel.value = true;
  } else {
    // A busca falhou (o GET por ID retornou 404/500), então o modal não abre.
    console.warn("2. Falha ao obter detalhes completos. Modal não será aberto.");
  }
};

const fecharModalDetalhes = () => {
  personagemSelecionado.value = null;
  modalDetalhesVisivel.value = false;
};

const setFiltro = (filtro) => {
  // 1. Atualiza o estado visual do filtro
  filtroAtivo.value = filtro;

  // 2. Chama a função principal de carregamento com o novo filtro
  carregarPersonagens(filtro);
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
  carregarPersonagens(filtroAtivo.value);
});
</script>
