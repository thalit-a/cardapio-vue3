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
  <nav v-if="tela === 'cardapio'"class="bg-white sticky top-0 z-40 shadow px-0 py-4 overflow-x-auto">
  <ul class="flex flex-nowrap gap-4 justify-start min-w-max px-4">
    <li v-for="(pratos, categoria) in receitas" :key="categoria">
      <a
        href="#"
        @click.prevent="categoriaSelecionada(categoria)"
        :class="[
          'text-lg font-semibold transition whitespace-nowrap',
          categoria === categoriaVisivel
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
    <div v-for="pratos, categoria in receitas" :id="categoria" class="p-4 mx-4 mb-2 mt-10 bg-white rounded-lg border-2 border-black padding-top">
      <h1 class="mb-5 mt-0 text-4xl font-semibold font-mono italic text-black text-center text-shadow-lg text-shadow-yellow-300">{{ categoria }}</h1>
      <div class="grid grid-cols-2 gap-x-4 gap-y-5 justify-items-center">
        
        <div v-for="receita in pratos" :key="receita.id" class="flex items-center gap-2 max-w-xl bg-white border border-gray-200 rounded-lg shadow-sm dark:bg-yellow-200 dark:border-black hover:bg-white"
          @click.prevent="abrirModalProduto(receita)"
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

  <!-- Modal Produtos
   <template v-if="tela === 'modalProduto'">
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
                  <button type="button" class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:outline-hidden" @click="tela = 'cardapio'">
                    <span class="sr-only">Close</span>
                    <XMarkIcon class="size-6" aria-hidden="true" />
                  </button>
                </div>
                <div class="sm:flex sm:items-start">
                  <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                    <DialogTitle as="h3" class="mt-10 font-mono italic text-4xl font-semibold text-black text-shadow-lg text-shadow-yellow-300">Detalhes do produto</DialogTitle>
                    <div class="mt-2">
                      <img :src="produtoSelecionado.imagem" alt="Imagem do produto" class="w-32 h-32 mx-auto rounded-full mb-4" />
                      <h2 class="text-2xl font-semibold text-black mb-2">{{ produtoSelecionado.nome }}</h2>
                      <p class="text-sm text-gray-700 mb-4">{{ produtoSelecionado.descricao }}</p>
                      <p class="text-xl font-semibold text-black-600 mb-4">R$ {{ produtoSelecionado.preco.toFixed(2) }}</p>
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
                  <button class="bg-yellow-300 hover:bg-yellow-500 text-black font-bold py-2 px-6 shadow-md transition-all duration-200" @click="adicionarProdutoAoCarrinho(); notify()">
                    Adicionar ao carrinho R$ {{ (produtoSelecionado.preco * quantidadeSelecionada).toFixed(2) }}
                  </button>
                  <button class="bg-yellow-200 hover:bg-yellow-500 text-black font-bold py-0 px-6 shadow-md transition-all duration-200" @click="fecharModalProduto">
                    Voltar
                  </button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </template> -->

  <!-- Modal de remover item
  <template v-if="tela === 'modalRemover'">
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
                  <button type="button" class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:outline-hidden" @click="tela = 'cardapio'">
                    <span class="sr-only">Close</span>
                    <XMarkIcon class="size-6" aria-hidden="true" />
                  </button>
                </div>
                <div class="sm:flex sm:items-start">
                  <div class="mx-auto flex size-12 shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:size-10">
                    <ExclamationTriangleIcon class="size-6 text-red-600" aria-hidden="true" />
                  </div>
                  <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                    <DialogTitle as="h3" class="text-xl font-semibold mb-4 text-gray-800">Remover item</DialogTitle>
                    <div class="mt-2">
                      <p class="text-gray-600 mb-6">Tem certeza que deseja remover este item do carrinho?</p>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-4 sm:flex sm:flex-row-reverse">
                  <button type="button" class="inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-red-500 sm:ml-3 sm:w-auto" @click="removerConfirmado">Remover</button>
                  <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-xs ring-1 ring-gray-300 ring-inset hover:bg-gray-50 sm:mt-0 sm:w-auto"  @click="tela = 'cardapio'">Voltar</button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </template> -->

   <!-- Modal de confirmação para finalizar compra
  <template v-if="tela === 'modalFinalizarCompra'">
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
                  <button type="button" class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:outline-hidden" @click="tela = 'carrinho'">
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
                  <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-xs ring-1 ring-gray-300 ring-inset hover:bg-gray-50 sm:mt-0 sm:w-auto"  @click="tela = 'carrinho'">Voltar</button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </template> -->
  
  <!-- Modal de sucesso da compra
  <template v-if="tela === 'modalSucessoCompra'">
  <TransitionRoot as="template" :show="true">
    <Dialog class="relative z-10" @close="tela.value = 'cardapio'">
      <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500/75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-sm sm:p-6">
              <div>
                <div class="mx-auto flex size-12 items-center justify-center rounded-full bg-green-100">
                  <CheckIcon class="size-20 text-green-600" aria-hidden="true" />
                </div>
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle as="h3" class="text-base font-semibold text-gray-900">Compra realizada! 🎉</DialogTitle>
                  <div class="mt-2">
                    <p class="text-sm text-gray-500">Seu pedido foi finalizado com sucesso. Obrigado por comprar conosco!</p>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <button type="button" class="inline-flex w-full justify-center rounded-md bg-yellow-300 hover:bg-yellow-200 text-black font-bold py-2 px-6 shadow-md" @click="fecharModalSucesso">Voltar ao cardápio</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template> -->

  <ModalSucessoCompra v-else-if="tela === 'modalSucessoCompra'"
  @fechar="tela = 'cardapio'"
  />
      
  <ModalFinalizarCompra v-else-if="tela === 'modalFinalizarCompra'"
    :carrinho="carrinho"
    @fechar="tela = 'carrinho'"
    @finalizarCompraConfirmado="finalizarCompraConfirmado"
  />

  <ModalRemoverProduto v-else-if="tela === 'modalRemoverProduto'"
    :carrinho="carrinho"
    :itemParaRemover="itemSelecionado"
    :informacaoCarrinho="carrinho"
    @removerConfirmado="removerConfirmado($event)"
    @fechar="tela = 'carrinho'"
  />

  <ModalProduto v-else-if="tela === 'modalProduto'"
  :produtoSelecionado="produtoSelecionado"
  :quantidadeSelecionada="quantidadeSelecionada"
  @fechar="tela = 'cardapio'"
  @adicionarProdutoAoCarrinho="adicionaCarrinho"
  />

  <DetalhesProduto v-else-if="tela === 'detalhes'"
    :name="produtoSelecionado.nome"
    :descricao="produtoSelecionado.descricao"
    :prepTimeMinutes="produtoSelecionado.preco"
    :imagem="produtoSelecionado.imagem"
    @fechar="tela = 'cardapio'"
    @foiAdicionado="adicionaCarrinho"
    />

  <CarrinhoComponent v-else-if="tela === 'carrinho'"
    :informacaoCarrinho="carrinho"
    @abrirModalRemover="abrirModalRemoverProduto($event)"
    @finalizarCompra="pedirConfirmacaoFinalizar"
    @fechar="tela = 'cardapio'"
    @voltar="tela = 'cardapio'"
  />
</template>

<script setup>
import { ref, onMounted, nextTick, watch } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { ExclamationTriangleIcon, CheckIcon } from '@heroicons/vue/24/outline'
import { Bars3Icon, XMarkIcon, ShoppingCartIcon, MapPinIcon, ClockIcon } from '@heroicons/vue/24/outline'
import DetalhesProduto from './DetalhesProduto.vue'
import CarrinhoComponent from './CarrinhoComponent.vue'
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
import ModalProduto from './ModalProduto.vue';
import ModalRemoverProduto from './ModalRemoverProduto.vue'
import ModalFinalizarCompra from './ModalFinalizarCompra.vue'
import ModalSucessoCompra from './ModalSucessoCompra.vue'
// fim da importaçÃo

const tela = ref('cardapio')
const receitas = ref({})
const produtoSelecionado = ref({})
const carrinho = ref({
  produtos: [],
  valor: 0,
 })

const navigation = [
  { name: 'Bebidas', href: '#' },
  { name: 'Entradas', href: '#' },
  { name: 'Menu Infantil', href: '#' },
  { name: 'Sobremesas', href: '#' }
]
const mobileMenuOpen = ref(false)

function pedirConfirmacaoRemover(index) {
  itemParaRemover.value = index
  tela.value = 'ModalRemoverProduto'
}

function abrirModalRemoverProduto(index) {
  itemSelecionado.value = index;
  tela.value = 'modalRemoverProduto';
}

function removerConfirmado(index) {

  if (index !== null && index >= 0) {
    // Remove completamente o item do carrinho
    carrinho.value.produtos.splice(index, 1);

    // Recalcula o valor total do carrinho
    carrinho.value.valor = carrinho.value.produtos.reduce(
      (total, p) => total + (p.valor * p.quantidade),
      0
    );
  }

  // Fecha o modal e limpa o índice do item para remoção
  itemParaRemover.value = null;
  tela.value = 'carrinho'
}

// funções para alterar a quantidade
function incrementar() {
  quantidadeSelecionada.value++
}

function decrementar() {
  if (quantidadeSelecionada.value > 1) {
    quantidadeSelecionada.value--
  }
}

function adicionarProdutoAoCarrinho() {
  const produto = {
    nome: produtoSelecionado.value.nome,
    imagem: produtoSelecionado.value.imagem,
    descricao: produtoSelecionado.value.descricao,
    valor: produtoSelecionado.value.preco,
    quantidade: quantidadeSelecionada.value
  }

  adicionaCarrinho(produto)
  tela.value = 'cardapio'
  quantidadeSelecionada.value = 1
}

const quantidadeSelecionada = ref(1)

// funcao da notificaçao
const notify = () => {
  toast.success("Produto adicionado ao carrinho!", {
    autoClose: 1500,
  }); // ToastOptions
}

// Função para abrir o modal de confirmação
function pedirConfirmacaoFinalizar() {
  if (carrinho.value.produtos.length === 0) {
    alert("Seu carrinho está vazio!");
    return;
  }
 // Abre o modal de confirmação
  tela.value = 'modalFinalizarCompra'
}

// Função para confirmar a finalização da compra
function finalizarCompraConfirmado() {
  // Limpar o carrinho após a compra
  carrinho.value.produtos = [];
  carrinho.value.valor = 0;

 // Abre o modal de sucesso
 tela.value = 'modalSucessoCompra'

}

function fecharModalSucesso() {
  tela.value = 'cardapio'
}

function fecharModalProduto() {
  tela.value = 'cardapio'
}

function configurarObservador() {
  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          categoriaVisivel.value = entry.target.id
        }
      })
    },
    { threshold: 0 }
  )

  nextTick(() => {
    Object.keys(receitas.value).forEach(categoria => {
      const el = document.getElementById(categoria)
      if (el) observer.observe(el)
    })
  })
}

// Watcher para reconfigurar o observer quando a tela for alterada para o cardápio
watch([tela, receitas], () => {
  if (tela.value === 'cardapio') {
    configurarObservador()
  }
}, { immediate: true }) // 'immediate: true' vai rodar a função logo ao montar

function categoriaSelecionada(categoria) {
  const el = document.getElementById(categoria)
  if (el) {
    el.scrollIntoView({
      behavior: 'smooth', // rolagem suave
      block: 'start'
    })
  }
}

function alterarQuantidade({ index, tipo }) {
  const item = carrinho.value.produtos[index]
  if (!item) return

  if (tipo === 'aumentar') {
    item.quantidade++
  } else if (tipo === 'diminuir' && item.quantidade > 1) {
    item.quantidade--
  }

  // Recalcular total
  carrinho.value.valor = carrinho.value.produtos.reduce(
    (total, item) => total + item.valor * item.quantidade,
    0
  )
}

function abrirModalProduto(receita) {
  produtoSelecionado.value = {
    nome: receita.name,
    descricao: receita.ingredients.join(', '),
    imagem: receita.image,
    preco: receita.prepTimeMinutes
  }
  quantidadeSelecionada.value = 1
  tela.value = 'modalProduto'
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

const itemSelecionado = ref(null)

const adicionaCarrinho = (produtoAdicionado) => {
  const existente = carrinho.value.produtos.find(p => p.nome === produtoAdicionado.nome)

  if (existente) {
    existente.quantidade += produtoAdicionado.quantidade
  } else {
    carrinho.value.produtos.push({...produtoAdicionado })
  }

  // Recalcula o valor total corretamente com base no valor unitário
  carrinho.value.valor = carrinho.value.produtos.reduce(
    (total, produto) => total + (produto.valor * produto.quantidade),
    0
  )
}

const categoriaVisivel = ref(null)

const itemParaRemover = ref(null)

const modalSucessoCompra = ref(false)

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

      // ⚠️ Agora que receitas foi preenchido, podemos observar as seções:
      configurarObservador()
    })
    .catch(err => console.error('Erro ao buscar receitas:', err))
}


onMounted(fetchData)

</script>
