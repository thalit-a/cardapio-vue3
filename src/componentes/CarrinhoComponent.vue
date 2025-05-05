<template>
  <div class="p-8 relative">
    <XMarkIcon class="absolute right-16 top-0 h-6 w-6 text-gray-500 cursor-pointer" @click.prevent="emit('fechar')" />

    <h1 class="mb-10 mt-6 font-mono italic text-4xl font-semibold text-black text-shadow-yellow-300 text-shadow-lg">Meu Carrinho</h1>

    <!-- Exibir os itens do carrinho se houver -->
    <div v-if="props.informacaoCarrinho.produtos.length > 0">
      <div v-for="(item, index) in props.informacaoCarrinho.produtos" :key="index" class="mb-8 border p-4 rounded-lg shadow-md">
        <div class="flex justify-between items-center mt-2">
          <img class="w-20 h-20 rounded-lg shadow-md" :src="item.imagem" alt="imagem do prato" />
          <span class="text-lg">Item: {{ item.nome }}</span>
          <div class="flex items-center gap-2"> Quantidade:
            <button @click="decrementar(index)" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded">
              -
            </button>

            <span class="flex items-center gap-2">{{ item.quantidade }}</span>

          <button @click="incrementar(index)" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded"> 
             +
            </button>
          </div>
          <span class="text-lg">Valor unitário: R$ {{ item.valor.toFixed(2) }}</span>
          <span class="text-lg">Valor total: R$ {{ (item.valor * item.quantidade).toFixed(2) }}</span>

          <button class="text-red-600 hover:bg-red-200 font-bold py-2 px-4 flex cursor-pointer" @click="pedirConfirmacaoRemover(index)">Remover</button>
        </div>
      </div>

      <button class="bg-yellow-300 hover:bg-yellow-200 text-black font-bold py-2 px-6 shadow-md"@click="emit('finalizarCompra')">Finalizar Compra</button>

    </div>

    <!-- Caso o carrinho esteja vazio -->
    <div v-else>
      <p class="text-xl">Seu carrinho está vazio.</p>
    </div>

    <!-- Total do carrinho -->
    <div class="mt-6 text-right text-2xl font-semibold text-black">
      Total do carrinho: R$ {{ calcularTotalCarrinho().toFixed(2) }}
    </div>
  </div>
</template>

<script setup>
import { XMarkIcon } from '@heroicons/vue/24/solid'
import { ref, onMounted } from 'vue'

// Definir props para acessar o carrinho
const props = defineProps({
  informacaoCarrinho: { type: Object, default: {} },
})

// Emissão de eventos para o componente pai
const emit = defineEmits(["removerItem", "fechar", "finalizarCompra"])

function pedirConfirmacaoRemover(index) {
  // Passando o índice correto para o método de remoção no componente pai
  emit('removerItem', index);
}

function pedirConfirmacaoFinalizar() {
  emit('finalizaCompra')
}

// Função para remover item do carrinho
function removerItem(index) {
  emit('removerItem', index); // Emitir evento para o componente pai
}

// Função para calcular o total do carrinho
function calcularTotalCarrinho() {
  return props.informacaoCarrinho.produtos.reduce((total, item) => {
    return total + (item.valor * item.quantidade)
  }, 0)
}

// Funções para alterar a quantidade
function incrementar(index) {
  props.informacaoCarrinho.produtos[index].quantidade++
}

function decrementar(index) {
  if (props.informacaoCarrinho.produtos[index].quantidade > 1) {
    props.informacaoCarrinho.produtos[index].quantidade--
  }
}

// Log para verificar as props ao carregar
onMounted(() => {
  console.log('props.informacaoCarrinho', props.informacaoCarrinho)
})
</script>
