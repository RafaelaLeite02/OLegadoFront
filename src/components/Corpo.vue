<template>
  <main class="flex items-center w-auto bg-stone-950 flex-col p-10 pt-40 min-h-screen">
    <h1 class="text-neutral-50 text-[50px]">
      Os <strong class="text-red-600 font-normal">Imortais</strong>
    </h1>
    <p class="text-neutral-50 text-[25px] m-5">
      Cada personagem carrega consigo séculos de história, poder e mistério.
      Explore suas origens, habilidades e os laços que os unem nesta saga eterna.
    </p>

    <section
      class="w-[105%] flex flex-col item-center text-center p-5 pt-17 bg-gradient-to-b from-stone-950 via-gray-900 to-stone-950">
      <div
        class="w-[19%] ml-[40%] h-15 flex flex-row justify-between text-center item-center rounded-full text-neutral-50 p-2">
        <a @click.prevent="setFiltro('Todos')" :class="{ 'border-red-700 text-red-700 ': filtroAtivo === 'Todos' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-19 p-2 hover:border-red-700 hover:text-red-700 transition cursor-pointer text-[22px]">Todos</a>
        <a @click.prevent="setFiltro('Livros')" :class="{ 'border-red-700 text-red-700': filtroAtivo === 'Livros' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-19 p-2 hover:border-red-700 hover:text-red-700 transition cursor-pointer text-[22px]">Livros</a>
        <a @click.prevent="setFiltro('Filme')" :class="{ 'border-red-700 text-red-700': filtroAtivo === 'Filme' }"
          class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-19 p-2 hover:border-red-700 hover:text-red-700 transition cursor-pointer text-[22px]">Filme</a>
      </div>
      <p class="text-neutral-50 m-5 text-[18px]">
        <strong class="text-red-600 font-normal">{{ personagens.length }}</strong> personagens
      </p>
    </section>

    <section class="flex flex-wrap m-6 items-center w-[90%] ml-130 ">
      <Card v-for="personagem in personagens" :key="personagem.id" :personagem="personagem"
        @abrir-modal="abrirModalComPersonagem" @deletar="deletarPersonagem" />
    </section>

    <Modal v-if="modalDetalhesVisivel" :personagem="personagemSelecionado" @fechar="fecharModalDetalhes"
      @deletar="deletarPersonagem" />

   <CriarPersonagem @personagem-criado="recarregarPersonagensEFechar" />

  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Card from "./Card.vue";
import CriarPersonagem from "./CriarPersonagem.vue";
import Modal from "./Modal.vue";
import api from "../services/api";

const personagens = ref([]);
const personagemSelecionado = ref(null); 
const modalDetalhesVisivel = ref(false); 
const modalCriarPersonagemVisivel = ref(false);
const filtroAtivo = ref('Todos');

async function carregarPersonagens(filtro = 'Todos') {
  try {
    const response = await api.get(`/Personagem?filtro=${filtro}`);
    personagens.value = response.data;
  } catch (error) {
    console.error("Erro ao carregar dados da API:", error);
  }
}

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
    if (confirm(`Tem certeza que deseja deletar ${personagemParaDeletar.name}?`)) {
      await api.delete(`/Personagem/${personagemParaDeletar.id}`); 
      await carregarPersonagens(); 
      fecharModalDetalhes(); 
    }
  } catch (error) {
    console.error("Erro ao deletar personagem:", error);
  }
};

const abrirModalComPersonagem = async (personagemDoCard) => {
  const idParaBuscar = personagemDoCard.id || personagemDoCard.Id;
  if (!idParaBuscar) {
    console.error("ID do Personagem inválido.");
    alert("Erro: ID do personagem não encontrado.");
    return;
  }

  const detalhes = await buscarDetalhesPersonagem(idParaBuscar);

  if (detalhes) {
    modalCriarPersonagemVisivel.value = false;
    personagemSelecionado.value = detalhes;
    modalDetalhesVisivel.value = true;
  }
};

const fecharModalDetalhes = () => {
  personagemSelecionado.value = null;
  modalDetalhesVisivel.value = false;
};

const setFiltro = (filtro) => {
  filtroAtivo.value = filtro;
  carregarPersonagens(filtro);
};

const recarregarPersonagensEFechar = async () => {
  await carregarPersonagens();
  fecharModalCriar();
};

const abrirModalCriar = () => {
  modalCriarPersonagemVisivel.value = true;
};

const fecharModalCriar = () => {
  modalCriarPersonagemVisivel.value = false;
};

onMounted(() => {
  carregarPersonagens(filtroAtivo.value);
});
</script>
