<template>
  <div class="p-8 relative">
    <XMarkIcon class="absolute right-16 top-0 h-6 w-6 text-gray-500 cursor-pointer" @click.prevent="emit('fechar')" />

    <h1 class="mb-10 mt-6 font-mono italic text-4xl font-semibold text-black text-shadow-yellow-300 text-shadow-lg">Meu Carrinho</h1>

    <!-- Exibir os itens do carrinho se houver -->
    <div v-if="props.informacaoCarrinho.produtos.length > 0">
      <div v-for="(produto, posicao) in props.informacaoCarrinho.produtos" :key="posicao" class="mb-8 border p-4 rounded-lg shadow-md">
        <div class="flex justify-between items-center mt-2">
          <img class="w-20 h-20 rounded-lg shadow-md" :src="produto.image" alt="imagem do prato" />
          <span class="text-lg">Produto: {{ produto.nome }}</span>
          <div class="flex produtos-center gap-2"> Quantidade:
            <button @click="decrementar(posicao)" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded">
              -
            </button>

            <span class="flex produtos-center gap-2">{{ produto.quantidade }}</span>

          <button @click="incrementar(posicao)" class="bg-yellow-200 hover:bg-yellow-300 text-black font-semibold px-3 py-1 rounded"> 
             +
            </button>
          </div>
          <span class="text-lg">Valor unitário: R$ {{ produto.valor.toFixed(2) }}</span>
          <span class="text-lg">Valor total: R$ {{ (produto.valor * produto.quantidade).toFixed(2) }}</span>
          <button class="text-red-600 hover:bg-red-200 font-bold py-2 px-4 flex cursor-pointer" @click="abrirModalRemover(produto, posicao)">Remover</button>
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
const emit = defineEmits(["abrirModalRemover", "fechar", "finalizarCompra"])

function abrirModalRemover(produto, posicao) {
  emit('abrirModalRemover', {produto, posicao});
}

// Função para calcular o total do carrinho
function calcularTotalCarrinho() {
  return props.informacaoCarrinho.produtos.reduce((total, produto) => {
    return total + (produto.valor * produto.quantidade)
  }, 0)
}

// Funções para alterar a quantidade
function incrementar(posicao) {
  props.informacaoCarrinho.produtos[posicao].quantidade++
}

function decrementar(posicao) {
  if (props.informacaoCarrinho.produtos[posicao].quantidade > 1) {
    props.informacaoCarrinho.produtos[posicao].quantidade--
  }
}

// Log para verificar as props ao carregar
onMounted(() => {
  console.log('props.informacaoCarrinho', props.informacaoCarrinho)
})
</script>
