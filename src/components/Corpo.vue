<template>
    <main class=" flex items-center w-auto bg-stone-950 flex-col p-8 pt-25 min-h-screen">
        <h1 class="text-neutral-50 text-[50px]  ">Os <strong class="text-red-600 font-normal">Imortais</strong></h1>
        <p class="text-neutral-50 text-[20px] m-5 ">Cada personagem carrega consigo seculos de historia, poder e
            misterio. Explore suas origens, habilidades e os laços que os unem nesta saga eterna.</p>
        <section
            class="w-[105%] flex flex-col item-center text-center p-5 pt-17 bg-gradient-to-b from-stone-950  via-gray-900 to-stone-950">
            <div
                class=" w-[19%] ml-[40%] h-15 flex flex-row justify-between text-center item-center rounded-full text-neutral-50 p-2">
                <a href="#" alt="todos"
                    class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2  hover:border-red-700 hover:border-b-2 hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200 duration-500 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)]">
                    Todos</a>
                <a href="#" alt="todos"
                    class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2  hover:border-red-700 hover:border-b-2 hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200 duration-500 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)]">
                    Livros</a>
                <a href="#" alt="todos"
                    class="flex border-b-2 border-neutral-500 text-neutral-500 h-11 w-16 p-2  hover:border-red-700 hover:border-b-2 hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200 duration-500 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)]">
                    Filme</a>
            </div>
            <p class="text-neutral-50 m-5"><strong class="text-red-600 font-normal"> {{ personagens.length }} </strong>
                personagens</p>
        </section>
        <section class="flex flex-wrap m-6 items-center w-[95%] ml-30">

            <section @click="abrirModalCriar" class="flex flex-wrap m-6 items-center w-[80%] ml-30">
                <Card v-for="personagem in personagens" :key="personagem.nome" :personagem="personagem"
                    @abrir-modal="abrirModalComPersonagem" />

            </section>

            <Modal :visivel="!!personagemSelecionado" :personagem="personagemSelecionado" @fechar="fecharModal"
                @deletar="deletarPersonagem" @editar="iniciarEdicao" />


        </section>
        <section>
            <CriarPersonagem v-if="modalCriarPersonagemVisivel" @close="fecharModalCriar"
                @personagem-criado="adicionarNovoPersonagem" />

            <div class="lista-de-cards">
                <Card v-for="p in personagens" :key="p.id" :personagem="p" @abrir-modal="abrirModalComPersonagem" />
            </div>
        </section>
        <CriarPersonagem :visivel="modalCriarPersonagemVisivel" :personagem-para-editar="personagemSendoEditado"
            @fechar-modal="fecharModalCriar" @personagem-criado="adicionarNovoPersonagem"
            @personagem-editado="atualizarPersonagem" />
    </main>
</template>

<script setup>
import { ref } from 'vue';
import Card from './Card.vue';
import CriarPersonagem from './CriarPersonagem.vue';
import Modal from './Modal.vue';



const personagens = ref([]);

const personagemSelecionado = ref(null);
const personagemSendoEditado = ref(null);
const modalCriarPersonagemVisivel = ref(false); // Nova variável de estado

const abrirModalComPersonagem = (personagem) => {
    personagemSelecionado.value = personagem;
};

const fecharModal = () => {
    personagemSelecionado.value = null;
};

const deletarPersonagem = (personagemParaDeletar) => {
    const index = personagens.value.findIndex(p => p.nome === personagemParaDeletar.nome);
    if (index !== -1) {
        personagens.value.splice(index, 1);
    }
    fecharModal();
};


const iniciarEdicao = (personagemParaEditar) => {
    personagemSendoEditado.value = personagemParaEditar;
    modalCriarPersonagemVisivel.value = true;
    fecharModal();
};

const atualizarPersonagem = (personagemAtualizado) => {
    const index = personagens.value.findIndex(p => p.nome === personagemAtualizado.nome);
    if (index !== -1) {
        personagens.value[index] = personagemAtualizado;
    }
    fecharModalCriar();
};

const adicionarNovoPersonagem = (novoPersonagem) => {
    personagens.value.push(novoPersonagem);
    fecharModalCriar();
};


const abrirModalCriar = () => {
    personagemSendoEditado.value = null;
    modalCriarPersonagemVisivel.value = true;
};

const fecharModalCriar = () => {
    modalCriarPersonagemVisivel.value = false;
};

</script>
