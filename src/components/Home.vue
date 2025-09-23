<template>
    <div class="w-auto h-220 bg-gradient-to-b from-stone-950  via-gray-800 to-stone-950 flex flex-col p-8">
        <div class=" flex flex-col justify-center p-30 items-center ">
            <div class="text-red-100 flex items-center justify-center">
                <img src="/public/img/coracaoicon.png" alt="coração" class="w-12 m-3" />
                <img src="/public/img/vampiroicon.png" alt="vampiro" class="w-18 m-3" />
                <img src="/public/img/coracaoicon.png" alt="coração" class="w-12 m-3" />
            </div>
            <h1 class="font-bold text-[85px] text-center ">
                <span class=" text-neutral-50 ">O Legado</span>
                <br>
                <span class="bg-gradient-to-r from-red-700 via-red-400 to-red-700 text-transparent bg-clip-text"> Of
                    Blood</span>
            </h1>
            <p class="text-center  text-neutral-50 p-10 text-[25px] w-[70%] ">Adentre o universo sombrio e sedutor dos
                imortais. Conheça os personagens que habitam as brumas eternas de <strong
                    class="text-red-600 font-normal">Forks</strong> e descubra seus segredos ancestrais.</p>
            <div class="flex flex-row justify-center item-center text-neutral-50 p-3 ">
                <div class=" flex border-1 rounded-full border-neutral-600 border-solid h-[41px] p-2 m-3">
                    <img src="/public/img/pessoas3.png" alt="pessoas" class="w-6 h-6 mr-2" />
                    Personagens
                </div>
                <div class=" flex border-1 rounded-full border-neutral-600 border-solid h-[40px] p-2 m-3">
                    <img src="/public/img/coroa.png" alt="coroa" class="w-5 h-5 mr-2" />
                    Vampiros
                </div>
                <div class=" flex border-1 rounded-full border-neutral-600 border-solid h-[40px] p-2 m-3">
                    <img src="/public/img/raioicon.png" alt="raio" class="w-5 h-5 m-1" />
                    Poder Total
                </div>
            </div>
        </div>
    </div>
    <hr class="h-1 border-0 bg-gradient-to-r from-stone-950 via-red-700 to-stone-950">
</template>

<script>
export default {
    name: 'Home',

}
</script>
