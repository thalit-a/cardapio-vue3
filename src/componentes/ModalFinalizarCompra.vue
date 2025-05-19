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
            <div className="sm:flex sm:items-start">
                <div className="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-green-100 sm:mx-0 sm:h-10 sm:w-10">
                <CheckIcon aria-hidden="true" className="h-6 w-6 text-green-500" />
                </div>
                <div className="mt-4 text-center sm:ml-4 sm:mt-0 sm:text-left">
                <DialogTitle as="h3" className="text-lg font-medium leading-6 text-gray-900">
                    Finalizar Compra
                </DialogTitle>
                <div className="mt-2">
                    <p className="text-sm text-gray-500">
                    Tem certeza que deseja finalizar a compra?
                    </p>
                </div>
                </div>
            </div>
            <div class="mt-5 sm:mt-4 sm:flex sm:flex-row-reverse">
                <button type="button" class="inline-flex w-full justify-center rounded-md bg-green-500 px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-green-300 sm:ml-3 sm:w-auto" @click="finalizarCompraConfirmado">Confirmar</button>
                <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-xs ring-1 ring-gray-300 ring-inset hover:bg-gray-50 sm:mt-0 sm:w-auto"  @click.prevent="emit('fechar')">Voltar</button>
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
import { XMarkIcon, CheckIcon } from '@heroicons/vue/24/outline'

const emit = defineEmits(['fechar', 'finalizarCompraConfirmado'])
const carrinho = ref({
  produtos: [],
  valor: 0,
 })

function finalizarCompraConfirmado() {
    emit('finalizarCompraConfirmado')
  carrinho.value.produtos = []
  carrinho.value.valor = 0

}

</script>


