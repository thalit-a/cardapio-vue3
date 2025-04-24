<template>
  <header class="bg-yellow-300">
    <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8" aria-label="Global">
      <div class="flex lg:flex-1">
        <a href="#" class="-m-1.5 p-1.5">
          <span class="sr-only">Solzinho</span>
          <img class="h-8 w-auto" src="/images/pngtree-cartoon-cute-little-sun-png-image_17702533.png" alt="Solzinho" />
        </a>
      </div>
      <div class="flex lg:hidden">
        <button type="button" class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-400" @click="mobileMenuOpen = true">
          <span class="sr-only">Open main menu</span>
          <Bars3Icon class="size-6" aria-hidden="true" />
        </button>
      </div>
      <div class="hidden lg:flex lg:gap-x-12">
        <a v-for="item in navigation" :key="item.name" :href="item.href" class="text-sm/6 font-semibold text-gray">{{ item.name }}</a>
      </div>
      <div class="hidden lg:flex lg:flex-1 lg:justify-end">
        <a href="#" class="text-sm/6 font-semibold text-white">Log in <span aria-hidden="true">&rarr;</span></a>
      </div>
    </nav>

    <Dialog class="lg:hidden" @close="mobileMenuOpen = false" :open="mobileMenuOpen">
      <div class="fixed inset-0 z-10" />
      <DialogPanel class="fixed inset-y-0 right-0 z-10 w-full overflow-y-auto bg-yellow-300 px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-white/10">
        <div class="flex items-center justify-between">
          <a href="#" class="-m-1.5 p-1.5">
            <span class="sr-only">Your Company</span>
            <img class="h-8 w-auto" src="/images/pngtree-cartoon-cute-little-sun-png-image_17702533.png" alt="" />
          </a>
          <button type="button" class="-m-2.5 rounded-md p-2.5 text-gray-400" @click="mobileMenuOpen = false">
            <span class="sr-only">Close menu</span>
            <XMarkIcon class="size-6" aria-hidden="true" />
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/25">
            <div class="space-y-2 py-6">
              <a v-for="item in navigation" :key="item.name" :href="item.href" class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-white hover:bg-yellow-200">{{ item.name }}</a>
            </div>
            <div class="py-6">
              <a href="#" class="-mx-3 block rounded-lg px-3 py-2.5 text-base/7 font-semibold text-white hover:bg-yellow-200">Conecte-se</a>
            </div>
          </div>
        </div>
      </DialogPanel>
    </Dialog>
    <div v-if="tela === 'cardapio'" class="relative isolate overflow-hidden bg-yellow-300 px-6 py-20 sm:py-8 lg:px-8">
      <img src="https://png.pngtree.com/thumb_back/fw800/background/20230806/pngtree-child-s-lunch-box-plate-to-serve-breakfast-image_12978907.jpg" alt="imagem de fundo" class="absolute inset-0 -z-10 size-full object-cover" />
      <div class="w-20 h-20 bg-yellow-200 p-4 rounded-lg flex justify-center items-center mx-auto border-4 border-white">
        <img class="h-8 w-auto mx-auto" src="/images/pngtree-cartoon-cute-little-sun-png-image_17702533.png" alt="Solzinho" />
      </div>
      <div class="mx-auto text-center justify-center items-center">
        <h2 class="mt-4 mb-4 text-7xl font-semibold font-mono italic text-white text-center text-shadow-lg text-shadow-black">Marmitaria Fazendinha</h2>
      </div>
      <div class="flex items-center justify-center gap-3">
        <MapPinIcon class="size-7" aria-hidden="true"/>
        <p class="mb-2 text-2xl font-mono italic text-white text-center text-shadow-lg text-shadow-black">Rua do bobos, Número zero</p>
      </div>
      <div class="flex justify-center">
        <p class="text-2xl font-mono italic text-green-700 text-center bg-white rounded-lg px-3 py-1 shadow-lg">Aberto</p>
      </div>
      <div class="flex items-center justify-center gap-3">
        <ClockIcon class="size-7" aria-hidden="true"/>
        <p class="mb-2 text-2xl font-mono italic text-white text-center text-shadow-lg text-shadow-black">40-60 min ● Mínimo R$30,00 </p>
      </div>
    </div>
  </header>

    <div v-if="tela === 'cardapio'" class="fixed bottom-6 right-6 bg-white shadow-lg rounded-xl p-6 w-40 flex flex-col items-center space-y-4 z-50">
    <ShoppingCartIcon class="size-6 text-yellow-500" aria-hidden="true" />

      <h2 class="text-1xl font-bold text-gray-800 font-mono">Carrinho</h2>

      <p class="text-lg text-gray-600">
        Total: <span class="font-semibold text-black">R$ {{ carrinho.valor.toFixed(2) }}</span>
      </p>

      <button class="bg-yellow-400 hover:bg-yellow-500 text-black font-bold py-0 px-6 rounded-full shadow-md transition-all duration-200"@click.prevent="abrirCarrinho()">
        Abrir carrinho
      </button>
    </div>

  <!-- MENU DE CATEGORIAS INICIADO  AQUI -->
  <nav class="bg-white sticky top-0 z-40 shadow px-0 py-4 overflow-x-auto">
  <ul class="flex flex-nowrap gap-4 justify-start min-w-max px-4">
    <li v-for="(pratos, categoria) in receitas" :key="categoria">
      <a
        href="#"
        @click.prevent="selecionarCategoria(categoria)"
        :class="[
          'text-lg font-semibold transition whitespace-nowrap',
          categoria === categoriaSelecionada
            ? 'text-yellow-500 underline underline-offset-4 decoration-2'
            : 'text-black hover:text-yellow-500'
        ]"
      >
        {{ categoria }}
      </a>
    </li>
  </ul>
</nav>




  <div v-if="tela === 'cardapio'">
    <div v-for="pratos, categoria in receitas" :id="categoria" class="p-4 mx-4 mb-2 mt-10 bg-white rounded-lg border-2 border-black padding">
      <h1 class="mb-5 mt-0 text-4xl font-semibold font-mono italic text-black text-center text-shadow-lg text-shadow-yellow-300">{{ categoria }}</h1>
      <div class="grid grid-cols-2 gap-x-4 gap-y-5 justify-items-center">
        
        <div v-for="receita in pratos" :key="receita.id" class="flex items-center gap-2 max-w-xl bg-white border border-gray-200 rounded-lg shadow-sm dark:bg-yellow-200 dark:border-black hover:bg-white"
          @click.prevent="abrirDetalhes(receita)"
        >
            <img class="rounded-full w-40 h-40" :src="receita.image" alt="Imagem da receita" />
            <div class="flex gap-4 p-4">
              <div class="flex flex-col flex-1">
                <h5 class="text-2xl font-semibold font-mono italic text-black text-center">{{ receita.name }}</h5>
                <span class="mt-2 font-mono italic text-sm text-black text-justify">
                  {{ receita.ingredients.join(', ') }}
                </span>

                <p class="mt-2 font-semibold text-black">
                  R$ {{ receita.prepTimeMinutes.toFixed(2) }}
                </p>
              </div>
              </div>

        </div>
      </div>
    </div>
  </div>

  <!-- Modal de confirmação para remover item -->
  <div v-if="modalRemover" class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg w-96 text-center">
      <h2 class="text-xl font-semibold mb-4 text-gray-800">Remover item</h2>
      <p class="text-gray-600 mb-6">Tem certeza que deseja remover este item do carrinho?</p>
      
      <div class="flex justify-center gap-4">
        <button
          class="px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700"
          @click="removerConfirmado"
        >
          Remover
        </button>
        <button
          class="px-4 py-2 bg-gray-300 text-gray-800 rounded hover:bg-gray-400"
          @click="modalRemover = false"
        >
          Cancelar
        </button>
      </div>
    </div>
  </div>

  <!-- Modal de confirmação para finalizar compra -->
<div v-if="modalFinalizarCompra" class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center z-50">
  <div class="bg-white p-6 rounded-lg shadow-lg w-96 text-center">
    <h2 class="text-xl font-semibold mb-4 text-gray-800">Finalizar Compra</h2>
    <p class="text-gray-600 mb-6">Tem certeza que deseja finalizar a compra?</p>

    <div class="flex justify-center gap-4">
      <button
        class="px-4 py-2 bg-green-600 text-white rounded hover:bg-green-700"
        @click="finalizarCompraConfirmado"
      >
        Confirmar
      </button>
      <button
        class="px-4 py-2 bg-gray-300 text-gray-800 rounded hover:bg-gray-400"
        @click="modalFinalizarCompra = false"
      >
        Cancelar
      </button>
    </div>
  </div>
</div>

<!-- Modal de sucesso da compra -->
<div v-if="modalSucessoCompra" class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center z-50">
  <div class="bg-white p-6 rounded-lg shadow-lg w-96 text-center">
    <h2 class="text-2xl font-bold mb-4 text-green-600">Compra realizada! 🎉</h2>
    <p class="text-gray-700 mb-6">Seu pedido foi finalizado com sucesso. Obrigado por comprar conosco!</p>

    <button
      class="px-6 py-2 bg-yellow-400 text-black font-bold rounded hover:bg-yellow-500"
      @click="fecharModalSucesso"
    >
      Voltar ao cardápio
    </button>
  </div>
</div>


  <DetalhesProduto v-else-if="tela === 'detalhes'"
    :name="produtoSelecionado.nome"
    :descricao="produtoSelecionado.descricao"
    :prepTimeMinutes="produtoSelecionado.preco"
    :imagem="produtoSelecionado.imagem"
    @fechar="tela = 'cardapio'"
    @foiAdicionado="adicionaCarrinho"
   />

  <CarrinhoComponent v-else-if="tela === 'carrinho'"
    :informacaoCarrinho="carrinho "
    @removerItem="pedirConfirmacaoRemover"
    @finalizarCompra="pedirConfirmacaoFinalizar"
    @fechar="tela = 'cardapio'"
    @voltar="tela = 'cardapio'"
  />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Dialog, DialogPanel } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon, ShoppingCartIcon, MapPinIcon, ClockIcon } from '@heroicons/vue/24/outline'
import DetalhesProduto from './DetalhesProduto.vue'
import CarrinhoComponent from './CarrinhoComponent.vue'
// fim da importaçÃo

const tela = ref('cardapio')
const receitas = ref({})
const produtoSelecionado = ref({})
const carrinho = ref({
  produtos: [],
  valor: 0
})

const navigation = [
  { name: 'Bebidas', href: '#' },
  { name: 'Entradas', href: '#' },
  { name: 'Menu Infantil', href: '#' },
  { name: 'Sobremesas', href: '#' }
]
const mobileMenuOpen = ref(false)

const fetchData = () => {
  fetch('https://dummyjson.com/recipes')
    .then(res => res.json())
    .then(data => {
      const agrupado = {}
      data.recipes.forEach(r => {
        if (!agrupado[r.cuisine]) agrupado[r.cuisine] = []
        agrupado[r.cuisine].push(r)
      })
      receitas.value = agrupado
    })
    .catch(err => console.error('Erro ao buscar receitas:', err))
}

function pedirConfirmacaoRemover(index) {
  itemParaRemover.value = index
  modalRemover.value = true
}

function removerConfirmado() {
  const index = itemParaRemover.value; // Pegue o índice do item a ser removido
  if (index !== null) {
    const produto = carrinho.value.produtos[index];

    // Remova o item corretamente do carrinho
    if (produto.quantidade > 1) {
      produto.quantidade--; // Apenas diminui a quantidade se for maior que 1
    } else {
      carrinho.value.produtos.splice(index, 1); // Remove o item se a quantidade for 1
    }

    // Recalcula o valor total do carrinho
    carrinho.value.valor = carrinho.value.produtos.reduce(
      (total, p) => total + (p.valor * p.quantidade),
      0
    );
  }

  // Fecha o modal e limpa o índice do item para remoção
  modalRemover.value = false;
  itemParaRemover.value = null;
}

// Variáveis de controle de estado
const modalFinalizarCompra = ref(false)

// Função para abrir o modal de confirmação
function pedirConfirmacaoFinalizar() {
  if (carrinho.value.produtos.length === 0) {
    alert("Seu carrinho está vazio!");
    return;
  }
  modalFinalizarCompra.value = true; // Abre o modal de confirmação
}

// Função para confirmar a finalização da compra
function finalizarCompraConfirmado() {
  // Limpar o carrinho após a compra
  carrinho.value.produtos = [];
  carrinho.value.valor = 0;

  // Fechar o modal
  modalFinalizarCompra.value = false;

 // Abre o modal de sucesso
 modalSucessoCompra.value = true

  // Voltar para o cardápio
  tela.value = 'cardapio';
}

function fecharModalSucesso() {
  modalSucessoCompra.value = false
  tela.value = 'cardapio'
}

const abrirDetalhes = (receita) => {
  tela.value = 'detalhes';
  produtoSelecionado.value = {
    nome: receita.name,
    descricao: receita.ingredients,
    imagem: receita.image,
    preco: receita.prepTimeMinutes,
    categoria: receita.cuisine
  };
}

const abrirCarrinho = () =>{
  tela.value = 'carrinho';
}

const adicionaCarrinho = (produtoAdicionado) => {
  const existente = carrinho.value.produtos.find(p => p.nome === produtoAdicionado.nome)

  if (existente) {
    // Aumenta a quantidade do item, mantém o valor unitário
    existente.quantidade += 1
  } else {
    // Adiciona novo produto com quantidade inicial de 1
    carrinho.value.produtos.push({
      ...produtoAdicionado,
      quantidade: 1
    })
  }

  // Recalcula o valor total corretamente com base no valor unitário
  carrinho.value.valor = carrinho.value.produtos.reduce(
    (total, produto) => total + (produto.valor * produto.quantidade),
    0
  )
}

const categoriaSelecionada = ref(null)

function selecionarCategoria(categoria) {
  categoriaSelecionada.value = categoria
  // Vai me levar até a categoria
  const el = document.getElementById(categoria)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}


const modalRemover = ref(false)

const itemParaRemover = ref(null)

const modalSucessoCompra = ref(false)

onMounted(fetchData)
</script>
