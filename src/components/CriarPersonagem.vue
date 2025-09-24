<template>
    <div>
        <section @click="abrirModal" class="w-160 flex flex-col item-center text-center p-5 pt-15  ">
            <button
                class="text-neutral-300 border-0 bg-gradient-to-r from-stone-950 via-gray-900 to-stone-950 text-xl  hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200 duration-300 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)] cursor-pointer">Adicionar
                Personagem</button>
        </section>

        <div v-if="modalAberto" class="fixed inset-0 z-50 flex items-center justify-center bg-gradient-to-b from-stone-950  via-red-950 to-stone-950 bg-opacity-75">
            <div
                class="w-full max-w-4xl overflow-y-auto scroll-smooth rounded-xl bg-stone-950 shadow-2xl flex flex-col max-h-[90vh]">

                <div class="relative p-8">
                    <button @click="fecharModal"
                        class="absolute right-6 top-6 text-gray-400 hover:text-white transition-colors duration-200">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24"
                            stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>

                    <h2 class="mb-10 text-3xl font-bold text-center text-neutral-300">Adicione o personagem</h2>

                    <form @submit.prevent="salvarPersonagem" class="space-y-6">
                        <div class="flex flex-col items-center mb-5">
                            <label for="foto" class="block text-[15px] font-medium text-gray-300 mb-3">Foto do
                                Personagem</label>
                            <div
                                class="relative w-40 h-40 rounded-full border-4 border-red-900 overflow-hidden flex items-center justify-center bg-gray-800">
                                <img v-if="urlFotoPreview" :src="urlFotoPreview" alt="Prévia da Foto"
                                    class="absolute inset-0 w-full h-full object-cover">
                                <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-20 w-20 text-gray-500"
                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-2-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                                </svg>
                                <input type="file" id="foto" name="foto" @change="handleFileUpload"
                                    class="absolute inset-0 w-full h-full opacity-0 cursor-pointer">
                            </div>
                            <p class="mt-3 text-[15px] text-gray-400">Clique na área acima para carregar uma imagem</p>
                        </div>

                        <div class="w-[100%] rounded-xl shadow-lg mb-10 mt-20">
                            <div class="flex flex-col sm:flex-row gap-6">
                                <div class="w-full sm:w-1/2">
                                    <label for="filtro-tipo" class="block text-sm font-medium text-gray-300 mb-2">A onde
                                        aparece</label>
                                    <select id="filtro-tipo" name="filtro-tipo" v-model="tipoSelecionado"
                                        class="w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50">
                                        <option value="" disabled selected>Escolha o tipo...</option>
                                        <option value="livro">Livro</option>
                                        <option value="filme">Filme</option>
                                        <option value="livroEfilme">Livro e Filme</option>
                                    </select>
                                </div>

                                <div class="w-full sm:w-1/2" v-if="tipoSelecionado">
                                    <label for="filtro-titulo"
                                        class="block text-sm font-medium text-gray-300 mb-2">Título</label>
                                    <select id="filtro-titulo" name="filtro-titulo" v-model="tituloSelecionado"
                                        class="w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50">
                                        <option value="" disabled selected>Escolha o título...</option>
                                        <option v-for="titulo in titulosDisponiveis" :key="titulo" :value="titulo">
                                            {{ titulo }}
                                        </option>
                                    </select>
                                </div>
                            </div>
                        </div>


                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10 mt-10">
                            <div> <label for="nome" class="block text-sm font-medium text-gray-300">Nome do
                                    Personagem</label>
                                <input type="text" id="nome" name="nome" v-model="form.nome"
                                    class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                    placeholder="Ex: Edward Anthony Cullen">
                            </div>
                            <div>
                                <label for="idade" class="block text-sm font-medium text-gray-300">Idade</label>
                                <input type="text" id="idade" name="idade" v-model="form.idade"
                                    class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                    placeholder="Ex: 17 anos (aparenta)">
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10 mt-10">
                            <div> <label for="tipoCriatura" class="block text-sm font-medium text-gray-300">Tipo de
                                    Criatura</label>
                                <input type="text" id="tipoCriatura" name="tipoCriatura" v-model="form.tipoCriatura"
                                    class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                    placeholder="Ex: Vampiro">
                            </div>
                            <div>
                                <label for="cla" class="block text-sm font-medium text-gray-300">Cla / Familia</label>
                                <input type="text" id="cla" name="cla" v-model="form.cla"
                                    class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                    placeholder="Ex: Cullen">
                            </div>
                        </div>

                        <div class="mb-10 mt-10">
                            <label for="biografia" class="block text-sm font-medium text-gray-300">História &
                                Biografia</label>
                            <textarea id="biografia" name="biografia" v-model="form.biografia" rows="5"
                                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                placeholder="Insira a biografia do personagem..."></textarea>
                        </div>

                        <div class="mb-10 mt-10">
                            <label for="habilidades" class="block text-sm font-medium text-gray-300">Habilidades &
                                Poderes (separar por vírgula)</label>
                            <input type="text" id="habilidades" name="habilidades" v-model="form.habilidades"
                                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                placeholder="Ex: Leitura Mental, Velocidade Sobre-humana, Força Vampírica">
                        </div>

                        <div class="mb-10 mt-10">
                            <label for="personalidade" class="block text-sm font-medium text-gray-300">Personalidade
                                (separar por vírgula)</label>
                            <input type="text" id="personalidade" name="personalidade" v-model="form.personalidade"
                                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                placeholder="Ex: Protetor, Melancólico">
                        </div>

                        <div class="mb-10 mt-10">
                            <label for="nivel_poder" class="block text-sm font-medium text-gray-300">Nível de Poder
                                (1-10)</label>
                            <input type="number" id="nivel_poder" name="nivel_poder" v-model.number="form.nivelPoder"
                                min="1" max="10"
                                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                                placeholder="Ex: 9">
                        </div>

                        <div class="flex justify-center pt-4 item-center text-center  w-[] ">
                            <button type="submit"
                                class="text-neutral-300 border-0 bg-gradient-to-r from-stone-950 via-gray-900 to-stone-950 text-xl  hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200 duration-200 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)] cursor-pointer font-bold">Adicionar
                                Personagem
                            </button>
                        </div>

                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const modalAberto = ref(false);
const urlFotoPreview = ref(null);
const form = ref({
    nome: '',
    titulo: '',
    idade: '',
    tipoCriatura: '',
    cla: '',
    biografia: '',
    habilidades: '',
    personalidade: '',
    nivelPoder: 1,
    foto: null
});


const tipoSelecionado = ref('');
const tituloSelecionado = ref('');
const titulosDisponiveis = ref([]);

const dados = {
    livro: ['Crepúsculo', 'Lua Nova', 'Eclipse', 'Amanhecer'],
    filme: ['Crepúsculo - O Filme', 'A Saga Crepúsculo: Lua Nova', 'A Saga Crepúsculo: Eclipse'],
    livroEfilme: ['Crepúsculo - O Filme', 'A Saga Crepúsculo: Lua Nova', 'A Saga Crepúsculo: Eclipse']
};

watch(tipoSelecionado, (novoTipo) => {
    tituloSelecionado.value = '';
    if (novoTipo) {
        titulosDisponiveis.value = dados[novoTipo];
    } else {
        titulosDisponiveis.value = [];
    }
});

const abrirModal = () => {
    modalAberto.value = true;
    resetForm();
};

const fecharModal = () => {
    modalAberto.value = false;
};

const handleFileUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
        form.value.foto = file;
        urlFotoPreview.value = URL.createObjectURL(file);
    } else {
        form.value.foto = null;
        urlFotoPreview.value = null;
    }
};

const salvarPersonagem = () => {
    console.log('Dados do Personagem:', form.value);
    console.log('Filtro de Tipo:', tipoSelecionado.value);
    console.log('Filtro de Título:', tituloSelecionado.value);
    alert('Personagem salvo! ');
    fecharModal();
};

const resetForm = () => {
    form.value = {
        nome: '',
        titulo: '',
        idade: '',
        tipoCriatura: '',
        cla: '',
        biografia: '',
        habilidades: '',
        personalidade: '',
        nivelPoder: 1,
        foto: null
    };
    urlFotoPreview.value = null;
    tipoSelecionado.value = '';
    tituloSelecionado.value = '';
};
</script>
