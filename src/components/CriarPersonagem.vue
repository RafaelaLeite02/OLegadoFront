<template>
  <div>

    <section @click="abrirModal" class="w-160 flex flex-col items-center text-center p-5 pt-15">
      <button
        class="text-neutral-300 border-0 bg-gradient-to-r from-stone-950 via-gray-900 to-stone-950 text-xl
               hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200
               duration-300 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)] cursor-pointer">
        Adicionar Personagem
      </button>
    </section>


    <div v-if="modalAberto"
      class="fixed inset-0 z-50 flex items-center justify-center bg-gradient-to-b from-stone-950 via-red-950 to-stone-950 bg-opacity-75">
      <div
        class="w-full max-w-4xl overflow-y-auto scroll-smooth rounded-xl bg-stone-950 shadow-2xl flex flex-col max-h-[90vh]">
        <div class="relative p-8">

          <button @click="fecharModal"
            class="absolute right-6 top-6 text-gray-400 hover:text-white transition-colors duration-200">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24"
              stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <h2 class="mb-10 text-3xl font-bold text-center text-neutral-300">Adicione o personagem</h2>

          <form @submit.prevent="salvarPersonagem" class="space-y-6">

            <div class="flex flex-col items-center mb-5">
              <label for="foto" class="block text-[15px] font-medium text-gray-300 mb-3">Foto do Personagem</label>
              <div
                class="relative w-40 h-40 rounded-full border-4 border-red-900 overflow-hidden flex items-center justify-center bg-gray-800">
                <img v-if="urlFotoPreview" :src="urlFotoPreview" alt="Prévia da Foto"
                  class="absolute inset-0 w-full h-full object-cover">
                <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-20 w-20 text-gray-500" fill="none"
                  viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-2-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <input type="file" id="foto" name="foto" @change="handleFileUpload"
                  class="absolute inset-0 w-full h-full opacity-0 cursor-pointer">
              </div>
              <p class="mt-3 text-[15px] text-gray-400">Clique na área acima para carregar uma imagem</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10 mt-10">

              <div>
                <label for="fonteMidia" class="block text-sm font-bold mb-2 text-neutral-300">
                  Origem da Mídia
                </label>
                <select id="fonteMidia" v-model="form.fonteMidia"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50">
                  <option value="Livros">Livro</option>
                  <option value="Filme">Filme</option>
                  <option value="Ambos">Ambos</option>
                </select>
              </div>

              <div>
                <label for="fonteId" class="block text-sm font-bold mb-2 text-neutral-300">
                  Título Específico
                </label>

                <select v-if="form.fonteMidia === 'Livros'" id="livroId" v-model="form.livroId"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50">
                  <option :value="null" disabled>Selecione o Livro</option>
                  <option v-for="livro in listaLivros" :key="livro.id" :value="livro.id">
                    {{ livro.nome }}
                  </option>
                </select>

                <select v-else-if="form.fonteMidia === 'Filme'" id="filmeId" v-model="form.filmeId"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50">
                  <option :value="null" disabled>Selecione o Filme</option>
                  <option v-for="filme in listaFilmes" :key="filme.id" :value="filme.id">
                    {{ filme.nome }}
                  </option>
                </select>
              </div>
            </div>


            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10 mt-10">
              <div>
                <label for="nome" class="block text-sm font-medium text-gray-300">Nome do Personagem</label>
                <input type="text" id="nome" v-model="form.name"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                  placeholder="Ex: Edward Anthony Cullen">
              </div>
              <div>
                <label for="idade" class="block text-sm font-medium text-gray-300">Idade</label>
                <input type="text" id="idade" v-model="form.idade"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                  placeholder="Ex: 17 anos (aparenta)">
              </div>
            </div>


            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-10 mt-10">
              <div>
                <label for="tipoCriaturaNome" class="block text-sm font-medium text-gray-300">Tipo de Criatura</label>
                <input type="text" id="tipoCriaturaNome" v-model="form.tipoCriaturaNome"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                  placeholder="Ex: Vampiro">
              </div>
              <div>
                <label for="claNome" class="block text-sm font-medium text-gray-300">Cla / Família</label>
                <input type="text" id="claNome" v-model="form.claNome"
                  class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                  placeholder="Ex: Cullen">
              </div>
            </div>


            <div class="mb-10 mt-10">
              <label for="descricao" class="block text-sm font-medium text-gray-300">História & Biografia</label>
              <textarea id="descricao" v-model="form.descricao" rows="5"
                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                placeholder="Insira a biografia do personagem..."></textarea>
            </div>


            <div class="mb-10 mt-10">
              <label for="habilidades" class="block text-sm font-medium text-gray-300">Habilidades & Poderes (separar
                por vírgula)</label>
              <input type="text" id="habilidades" v-model="form.habilidades"
                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                placeholder="Ex: Leitura Mental, Velocidade Sobre-humana, Força Vampírica">
            </div>


            <div class="mb-10 mt-10">
              <label for="personalidade" class="block text-sm font-medium text-gray-300">Personalidade (separar por
                vírgula)</label>
              <input type="text" id="personalidade" v-model="form.personalidade"
                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                placeholder="Ex: Protetor, Melancólico">
            </div>


            <div class="mb-10 mt-10">
              <label for="nivel_poder" class="block text-sm font-medium text-gray-300">Nível de Poder (1-10)</label>
              <input type="number" id="nivel_poder" v-model.number="form.nivelPoder" min="1" max="10"
                class="mt-1 block w-full rounded-md bg-gray-800 border border-gray-700 text-white p-3 focus:border-red-500 focus:ring focus:ring-red-500 focus:ring-opacity-50"
                placeholder="Ex: 9">
            </div>


            <div class="flex justify-center pt-4">
              <button type="submit"
                class="text-neutral-300 border-0 bg-gradient-to-r from-stone-950 via-gray-900 to-stone-950 text-xl
                             hover:text-[18px] hover:text-red-700 hover:font-weight:900 transition-transform delay-200
                             duration-200 ease-in-out hover:scale-130 hover:[text-shadow:0px_0px_50px_rgba(255,255,255,0.6)] cursor-pointer font-bold">
                Adicionar Personagem
              </button>
            </div>

          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits, onMounted, reactive } from "vue";
import api from "../services/api";

const modalAberto = ref(false);
const urlFotoPreview = ref(null);
const listaLivros = ref([]);
const listaFilmes = ref([]);

const form = ref({
  name: "",
  idade: "",
  tipoCriaturaNome: "",
  claNome: "",
  descricao: "",
  poder: "",
  habilidades: "",
  personalidade: "",
  nivelPoder: 1,
  fotoURL: null,
  fonteMidia: 'Livros', // Valor padrão
  livroId: null,
  filmeId: null,
});

const emit = defineEmits(["personagem-criado"]);

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
    form.value.fotoURL = URL.createObjectURL(file); // preview
    urlFotoPreview.value = form.value.fotoURL;
  } else {
    form.value.fotoURL = null;
    urlFotoPreview.value = null;
  }
};

onMounted(async () => {
  try {
    // Assume que as rotas api/Livro/lista e api/Filme/lista estão prontas.
    const [resLivros, resFilmes] = await Promise.all([
      api.get('/Livro/lista'),
      api.get('/Filme/lista')
    ]);

    listaLivros.value = resLivros.data;
    listaFilmes.value = resFilmes.data;
  } catch (error) {
    console.error("Erro ao carregar listas de Livros/Filmes:", error);
  }
});


async function salvarPersonagem() {

  if (form.value.fonteMidia === 'Livros') {
    form.value.filmeId = null; // Zera o ID do filme
  } else if (form.value.fonteMidia === 'Filme') {
    form.value.livroId = null; // Zera o ID do livro
  }else if (form.value.fonteMidia === 'Ambos') {
  // aqui o usuário pode escolher os dois
  // então NÃO zeramos nada
  } else {
    form.value.livroId = null;
    form.value.filmeId = null;
  }

  const novoPersonagem = {
    name: form.value.name,
    fotoURL: form.value.fotoURL,
    idade: form.value.idade,
    poder: form.value.poder,
    descricao: form.value.descricao,
    claNome: form.value.claNome,
    tipoCriaturaNome: form.value.tipoCriaturaNome,
    habilidades: form.value.habilidades || "",
    personalidade: form.value.personalidade,
    nivelPoder: form.value.nivelPoder,
    livroId: form.value.livroId,
    filmeId: form.value.filmeId,
    fonteMidia: form.value.fonteMidia,

  };

  try {
    const response = await api.post("/Personagem", novoPersonagem); // ✅ usa api.js
    alert('Personagem criado com sucesso!');
    emit("personagem-criado", response.data);
    fecharModal();
    resetForm();
  } catch (error) {
    console.error("ERRO AO CRIAR PERSONAGEM:", error);

    if (error.response && error.response.data) {
      alert(`Falha ao criar personagem: ${JSON.stringify(error.response.data)}`);
    } else {
      alert('Falha ao conectar com a API. Verifique o console.');
    }
  }
}

const resetForm = () => {
  form.value = {
    name: "",
    idade: "",
    tipoCriaturaNome: "",
    claNome: "",
    descricao: "",
    poder: "",
    habilidades: "",
    personalidade: "",
    nivelPoder: 1,
    fotoURL: null,
    fonteMidia: 'Livros', // Resetar o filtro padrão
    livroId: null,
    filmeId: null,
  };
  urlFotoPreview.value = null;
};
</script>