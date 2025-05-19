<template>
<TransitionRoot as="template" :show="true">
    <Dialog class="relative z-10" @close="tela.value = 'cardapio'">
    <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500/75 transition-opacity" />
    </TransitionChild>

    <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
        <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pt-5 pb-4 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
            <div class="absolute top-0 right-0 hidden pt-4 pr-4 sm:block">
                <button type="button" class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:outline-hidden" @click.prevent="emit('fechar')">
                <span class="sr-only">Close</span>
                <XMarkIcon class="size-6" aria-hidden="true" />
                </button>
            </div>
            <div class="sm:flex sm:items-start">
                <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                <DialogTitle as="h3" class="mt-10 font-mono italic text-4xl font-semibold text-black text-shadow-lg text-shadow-yellow-300">Detalhes do produto</DialogTitle>
                <div class="mt-2">
                    <img :src="props.produtoSelecionado.imagem" alt="imagem do prato" class="w-32 h-32 mx-auto rounded-full mb-4" />
                    <h2 class="text-2xl font-semibold text-black mb-2">{{ props.produtoSelecionado.nome }}</h2>
                    <p class="text-sm text-gray-700 mb-4">{{ props.produtoSelecionado.descricao }}</p>
                    <p class="text-xl font-semibold text-black-600 mb-4">R$ {{ props.produtoSelecionado.preco.toFixed(2) }}</p>
                </div>
                </div>
            </div>
            <div class="flex justify-center items-center gap-4 mb-6">
                <button @click="decrementar" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded">
                -
                </button>

                <span class="text-lg font-bold">{{ quantidadeSelecionada }}</span>

                <button @click="incrementar" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded"> 
                +
                </button>
            </div>
            <div class="flex justify-center gap-4">
                <button class="bg-yellow-300 hover:bg-yellow-500 text-black font-bold py-2 px-6 shadow-md transition-all duration-200" @click="adicionarProdutoAoCarrinho(); notify(); emit('fechar')">
                Adicionar ao carrinho R$ {{ (props.produtoSelecionado.preco * quantidadeSelecionada).toFixed(2) }}
                </button>
                <button class="bg-yellow-200 hover:bg-yellow-500 text-black font-bold py-0 px-6 shadow-md transition-all duration-200" @click.prevent="emit('fechar')">
                Voltar
                </button>
            </div>
            </DialogPanel>
        </TransitionChild>
        </div>
    </div>
    </Dialog>
</TransitionRoot>
</template>

<script setup>
import { ref } from 'vue';
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'
import { toast } from 'vue3-toastify';


const props = defineProps({
    produtoSelecionado: { type: Object, default: {} },
})

const emit = defineEmits(["adicionarProdutoAoCarrinho", "fechar"])

function adicionarProdutoAoCarrinho() {
    const produto = {
        nome: props.produtoSelecionado.nome,
        quantidade: quantidadeSelecionada.value,
        valor: props.produtoSelecionado.preco,
        descricao: props.produtoSelecionado.descricao,
        image: props.produtoSelecionado.imagem
    }
    emit('adicionarProdutoAoCarrinho', produto)

}

const notify = () => {
  toast.success("Produto adicionado ao carrinho!", {
    autoClose: 1500,
  }); 
}

const quantidadeSelecionada = ref(1)

function incrementar() {
  quantidadeSelecionada.value++
}

function decrementar() {
  if (quantidadeSelecionada.value > 1) {
    quantidadeSelecionada.value--
  }
}
</script>