<template>
    <main class=" flex items-center w-auto h-500 bg-stone-950 flex-col p-8">
        <h1 class="text-neutral-50 text-[50px]  ">Os <strong class="text-red-600 font-normal">Imortais</strong></h1>
        <p class="text-neutral-50 text-[20px] m-5 ">Cada personagem carrega consigo seculos de historia, poder e
            misterio. Explore suas origens, habilidades e os laços que os unem nesta saga eterna.</p>
        <!--<section class="flex flex-col item-center justify-center text-center p-5">
            <div
                class=" w-100 h-15 bg-gradient-to-b from-stone-950  via-gray-900 to-stone-950 flex flex-row justify-between item-center rounded-full text-neutral-50 p-2">
                <a href="#" alt="todos" class="flex border-2 rounded-full border-neutral-600 border-solid h-12 w-24 p-2">
                    <img src="/public/img/playlist.png" alt="coração" class="w-6 h-6 mr-2" />Todos</a>
                <a href="#" alt="todos" class="flex border-1 rounded-full border-neutral-600 border-solid h-12 w-24 p-2"> <img
                        src="/public/img/bookmark.png" alt="coração" class="w-6 h-6 mr-2" />Livros</a>
                <a href="#" alt="todos" class="flex border-1 rounded-full border-neutral-600 border-solid h-12 w-24 p-2">
                    <img src="/public/img/video-editing.png" alt="coração" class="w-6 h-6 mr-2" />Filme</a>
            </div>
            <p class="text-neutral-50 m-6"><strong> 5 </strong>personagens</p>
        </section> -->
        <section class="flex flex-wrap m-6 items-center w-[80%] ml-30">

            <section class="relative w-90 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10">
                <div class="relative h-52">
                    <img src="/img/edward2.jpg" alt="FotoPersonagem" class="w-full h-full object-cover" />
                    <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

                    <div class="absolute border-1 rounded-full p-1 top-2 right-2 text-red-500 font-semibold text-sm">
                        Vampiro
                    </div>

                    <div class="absolute bottom-3 left-3">
                        <p class="text-yellow-400 font-semibold flex items-center">
                            Sininho
                        </p>
                        <h2 class="text-xl font-bold">Edward Cullen</h2>
                        <p class="text-sm text-gray-200">Família Cullen</p>
                    </div>
                </div>

                <div class="p-5 space-y-4">
                    <p class="text-sm text-gray-300">
                        Lindo e maravilhoso, incompreendido pela sociedade
                    </p>

                    <div>
                        <p class="text-xs uppercase text-gray-400">Idade:</p>
                        <p class="text-sm font-medium">Mais de 100 anos (aparenta 19)</p>
                    </div>

                    <div class="pt-3">
                        <button
                            class="w-full bg-gray-800 border border-gray-600 hover:bg-gray-700 text-sm py-2 rounded-lg transition">
                            Ver Perfil Completo

                        </button>
                    </div>
                </div>
            </section>

            <section class="relative w-96 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10">
                <div class="relative h-52">
                    <img src="/img/bella.webp" alt="FotoPersonagem" class="w-full h-full object-cover" />
                    <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

                    <div class="absolute border-1 rounded-full p-1 top-2 right-2 text-red-500 font-semibold text-sm">
                        Vampira
                    </div>

                    <div class="absolute bottom-3 left-3">
                        <p class="text-yellow-400 font-semibold flex items-center">
                            Sonsa
                        </p>
                        <h2 class="text-xl font-bold">Isabella Swan</h2>
                        <p class="text-sm text-gray-200">Família Cullen</p>
                    </div>
                </div>

                <div class="p-5 space-y-4">
                    <p class="text-sm text-gray-300">
                        Só quer ser uma vampira e quando conseguiu virou rara.
                    </p>

                    <div>
                        <p class="text-xs uppercase text-gray-400">Idade:</p>
                        <p class="text-sm font-medium">Mais de 100 anos (aparenta 19)</p>
                    </div>

                    <div class="pt-3">
                        <button
                            class="w-full bg-gray-800 border border-gray-600 hover:bg-gray-700 text-sm py-2 rounded-lg transition">
                            Ver Perfil Completo
                        </button>
                    </div>
                </div>
            </section>

            <section class="relative w-96 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10">
                <div class="relative h-52">
                    <img src="/img/alice.jpg" alt="FotoPersonagem" class="w-full h-full object-cover" />
                    <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

                    <div class="absolute border-1 rounded-full p-1 top-2 right-2 text-red-500 font-semibold text-sm">
                        Vampiro
                    </div>

                    <div class="absolute bottom-3 left-3">
                        <p class="text-yellow-400 font-semibold flex items-center">
                            Ver o futuro
                        </p>
                        <h2 class="text-xl font-bold">Alice Cullen</h2>
                        <p class="text-sm text-gray-200">Família Cullen</p>
                    </div>
                </div>

                <div class="p-5 space-y-4">
                    <p class="text-sm text-gray-300">
                        Maravilhosa, melhor personagem EVERRRRRR
                    </p>

                    <div>
                        <p class="text-xs uppercase text-gray-400">Idade:</p>
                        <p class="text-sm font-medium">Mais de 100 anos (aparenta 19)</p>
                    </div>

                    <div class="pt-3">
                        <button
                            class="w-full bg-gray-800 border border-gray-600 hover:bg-gray-700 text-sm py-2 rounded-lg transition">
                            Ver Perfil Completo
                        </button>
                    </div>
                </div>
            </section>

            <section class="relative w-96 rounded-2xl overflow-hidden shadow-xl bg-gray-900 text-white m-10">
                <div class="relative h-52">
                    <img src="/img/jasper.jpg" alt="FotoPersonagem" class="w-full h-full object-cover" />
                    <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>

                    <div class="absolute border-1 rounded-full p-1 top-2 right-2 text-red-500 font-semibold text-sm">
                        Vampiro
                    </div>

                    <div class="absolute bottom-3 left-3">
                        <p class="text-yellow-400 font-semibold flex items-center">
                            Convencer os seres
                        </p>
                        <h2 class="text-xl font-bold">Jasper Cullen</h2>
                        <p class="text-sm text-gray-200">Família Cullen</p>
                    </div>
                </div>

                <div class="p-5 space-y-4">
                    <p class="text-sm text-gray-300">
                        #SuperLegal sem comentarios para esse maravilhoso.
                    </p>

                    <div>
                        <p class="text-xs uppercase text-gray-400">Idade:</p>
                        <p class="text-sm font-medium">Mais de 100 anos (aparenta 19)</p>
                    </div>

                    <div class="pt-3">
                        <button
                            class="w-full bg-gray-800 border border-gray-600 hover:bg-gray-700 text-sm py-2 rounded-lg transition">
                            Ver Perfil Completo
                        </button>
                    </div>
                </div>
            </section>



        </section>
    </main>
</template>

<script>
export default {
    name: 'Corpo',
}
</script>

<style scoped></style>