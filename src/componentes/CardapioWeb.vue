<template>
  <header class="bg-yellow-300">
    <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8" aria-label="Global">
      <div class="flex lg:flex-1">
        <a href="#" class="-m-1.5 p-1.5">
          <span class="sr-only">Solzinho</span>
          <img class="h-8 w-auto" src="/images/pngtree-cartoon-cute-little-sun-png-image_17702533.png" alt="" />
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
  </header>


  <!-- botao que abre a notificaçÃo -->
  <button @click="notify">Notify !</button>

  <div class="p-4">

    
    <ShoppingCartIcon class="size-6" aria-hidden="true" />

    <h2 class="text-xl font-bold">Carrinho</h2>


    <!-- <pre>{{ carrinho }}</pre> -->
    <p class="mt-2">Total: R$ {{ carrinho.valor.toFixed(2) }}</p>
    <button class="bg-yellow-100 hover:bg-yellow-200 text-black font-bold py-2 px-4 rounded-full flex cursor-pointer" @click.prevent="abrirCarrinho()">Abrir carrinho</button>
  </div>

  <div v-if="tela === 'cardapio'">
    <div v-for="pratos, categoria in receitas" :id="categoria" class="bg-white rounded-lg shadow-sm">
      <h1 class="mb-10 mt-10 text-4xl font-semibold font-mono italic text-black text-center text-shadow-lg text-shadow-yellow-300">
        {{ categoria }}
      </h1>

      <div class="grid grid-cols-3 gap-8">
        
        <div v-for="receita in pratos" :key="receita.id" class="max-w-sm bg-white border border-gray-200 rounded-lg shadow-sm dark:bg-yellow-300 dark:border-black hover:scale-75 hover:bg-red-600"
          @click.prevent="abrirDetalhes(receita)"
        >
            <img class="rounded-t-lg" :src="receita.image" alt="Imagem da receita" />
            <div class="p-5">
              <h5 class="mb-2 text-2xl font-semibold font-mono italic text-black text-center">{{ receita.name }}</h5>
              <p class="mb-3 font-semibold text-black">R$ {{ receita.prepTimeMinutes.toFixed(2) }}</p>
            </div>
        </div>
      </div>
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
    @removerItem="removerDoCarrinho"
    @finalizarCompra="finalizarCompra"
    @fechar="tela = 'cardapio'"
    @voltar="tela = 'cardapio'"
  />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Dialog, DialogPanel } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon, ShoppingCartIcon } from '@heroicons/vue/24/outline'
import DetalhesProduto from './DetalhesProduto.vue'
import CarrinhoComponent from './CarrinhoComponent.vue'
// importaçÕes da notificaçÃo
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
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

function removerDoCarrinho(index) {
  if (confirm('Tem certeza que deseja remover este item?')) {
    // tirar o item do carrinho
    carrinho.value.produtos.splice(index, 1)
    // somar os valores restantes
    carrinho.value.valor = carrinho.value.produtos.reduce(
      (total, produto) => total + produto.valor,
      0
    )
  }
}

function finalizarCompra() {
  if (carrinho.value.produtos.length === 0) {
    alert("Seu carrinho está vazio!");
    return;
  }

  if (confirm("Deseja realmente finalizar a compra?")) {
    
    // depois que finalizar a compra o carrinho será zerado
    carrinho.value.produtos = [];
    carrinho.value.valor = 0;

    alert("Compra finalizada com sucesso! 🎉");

    // Volta para o cardápio
    tela.value = 'cardapio';
  }
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
  carrinho.value.produtos.push(produtoAdicionado)
  carrinho.value.valor += produtoAdicionado.valor
}

// funcao da notificaçao
const notify = () => {
  toast.success("Wow so easy !", {
    autoClose: 1500,
  }); // ToastOptions
}

onMounted(fetchData)
</script>
