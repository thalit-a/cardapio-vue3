<template>
    <div class="p-8 relative">
      <XMarkIcon class="absolute right-16 top-0 h-6 w-6 text-gray-500 cursor-pointer" @click.prevent="emit('fechar')"/>

      <h1 class="mb-10 mt-6 font-mono italic text-4xl font-semibold text-black text-shadow-yellow-300 text-shadow-lg">Meu Carrinho</h1>
      
      <!-- props.informacaoCarrinho = <pre>{{ props.informacaoCarrinho }}</pre> -->

      <!-- vai exibir se a lista de itens no carrinho for maior que zero-->
      <div v-if="props.informacaoCarrinho.produtos.length > 0">
        <div v-for="(item, index) in props.informacaoCarrinho.produtos" :key="index" class="mb-8 border p-4 rounded-lg shadow-md">
           
          <div class="flex justify-between items-center mt-2">
            <img class="w-20 h-20 rounded-lg shadow-md" :src="item.imagem" alt="imagem do prato" />
            <span class="text-lg">Item: {{ item.nome }}</span>
            <span class="text-lg">Quantidade: {{ item.quantidade }}</span>
            <span class="text-lg">Preço: {{ item.valor.toFixed(2) }}</span>

            <button class="text-red-600 hover:bg-red-200 font-bold py-2 px-4 flex cursor-pointer" @click="removerItem(index)">Remover</button>
          </div>
        </div>
  
        <button class="bg-yellow-300 hover:bg-yellow-200 text-black font-bold py-2 px-4 flex cursor-pointer" @click="finalizarCompra()">Finalizar Compra</button>
      </div>
  
      <!-- caso não haja itens no carrinho, será exibida essa mensagem -->
      <div v-else>
        <p class="text-xl">Seu carrinho está vazio.</p>
      </div>
    </div>
</template>
  
  <script setup>
  import { XMarkIcon } from '@heroicons/vue/24/solid'
  import { ref, onMounted } from 'vue'
  // aqui se define as variaveis que o componente vai receber, nesse caso, vai receber o nome do produto, o valor e a imagem
  const props = defineProps({
    informacaoCarrinho: { type: Object, default: {} },
  })
  // aqui é definido os emits, eles são o que envia a informação aqui de dentro do componente para o lado de fora
  const emit = defineEmits(["removerItem", "fechar","finalizarCompra"])

    // Remove item do carrinho
  function removerItem(index) {
    emit('removerItem', index)
  }
  
  function finalizarCompra(){
    emit('finalizarCompra')
  }

  onMounted(() => {
    console.log('props.informacaoCarrinho', props.informacaoCarrinho)
  })
</script>
  