<template>
    <div class="grid col-span-1 justify-items-center relative">
        <XMarkIcon class="absolute right-15 top-0 h-6 w-6 text-gray-500 cursor-pointer" @click.prevent="emit('fechar')"/>

        <span class="font-mono italic text-4xl font-semibold text-black text-shadow-lg text-shadow-yellow-300 ">Descrição do prato</span>

        <span class="mt-10 font-mono italic text-2xl text-black text-shadow-yellow-300 text-shadow-lg">{{ props.name }} - R${{ props.prepTimeMinutes.toFixed(2) }}</span>
        <div class="flex justify-center items-center mb-5 mt-10">
            <img class="w-80 h-80 rounded-lg shadow-md" :src="props.imagem" alt="imagem do prato" />
        </div>
        <span class="mt-5 mb-10 font-mono italic text-sm text-black text-center">
            {{ props.descricao.join(', ') }}
        </span>
        <button class="bg-yellow-100 hover:bg-yellow-200 text-black font-bold py-2 px-4 rounded-full flex items-center justify-center ml-6 cursor-pointer mb-10" @click.prevent="adicionar(); notify(), emit('fechar')"> <!-- ao clicar no botão chama a função adicionar -->
            <ShoppingCartIcon class="size-6" aria-hidden="true" />
            Adicionar ao carrinho
        </button>
    </div>
</template>

<script setup>
import { XMarkIcon } from '@heroicons/vue/24/solid'
import { ShoppingCartIcon } from '@heroicons/vue/24/outline'
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

// aqui se define as variaveis que o componente vai receber, nesse caso, vai receber o nome do produto, o valor e a imgem
const props = defineProps({
    name: { type: String, default: "" },
    descricao: { type: Array, default: [] },
    prepTimeMinutes: { type: Number, default: 0 },
    imagem: { type: String, default: "" },
})

// funcao da notificaçao
const notify = () => {
  toast.success("Produto adicionado ao carrinho!", {
    autoClose: 1500,
  }); // ToastOptions
}

// aqui é definido os emits, eles são o que envia a informação aqui de dentro do componente para o lado de fora
const emit = defineEmits(["foiAdicionado", "fechar"])

function adicionar() {
    emit("foiAdicionado", {
        nome: props.name,
        quantidade: 1,
        valor: props.prepTimeMinutes,
        descricao: props.descricao,
        imagem: props.imagem
    })
    // a função emit é quem comunica ao componente pai, ou seja, a "pagina" onde ela tá inserida que algo aconteceu.
    // a funcao emit tem 2 parametros, o primeiro, é a "acao" e o segundo parametro a informação
    // ex: emit( funcaoChamada, valor), o primeiro parametro é exatamente o que se deve procurar na declaração desse componente
}


</script>

