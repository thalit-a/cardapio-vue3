<template>
  <!-- Links -->
  <a href="#/" class="text-black-800 font-bold text-1xl text-center">Página 1</a>
  |
  <a href="#/pagina2" class="text-black-800 font-bold text-1xl text-center">Página 2</a>
  |
  <a href="#/HP" class="text-black-800 font-bold text-1xl text-center">Página 3</a>
 

  <!-- Exibição das páginas -->
  <component :is="currentView" />
</template>

<!-- Estrutura extraída do site: https://vuejs.org/guide/scaling-up/routing.html -->

<!-- SCRIPT -->
<script setup>
  // Importações do Vue
  import { ref, computed } from 'vue'

  // Páginas
  import Exemplo14 from './Exemplo14Receita.vue'
  import Pagina2 from './Pagina2.vue'
  import Pagina3 from './Pagina3.vue'
  import PaginaErro from './PaginaErro.vue'

  // Criar uma estrutura de rotas, contendo o caminho e o camponente (se na url conter somente uma barra [/] irá retornar página1, se tiver barra página 2 [/pagina2] irá retornar a página 2 e se não encontrar nenhum dos dois, será exibida a página de erro)
  const routes = {
    '/': Exemplo14,
    '/pagina2': Pagina2,
    '/HP': Pagina3,
    '/404': PaginaErro
  }

  // Obter o conteúdo a partir da cerquila, exemplo: http://localhost:5173/#/sobre o retorno será: #/sobre
  const referenciaRota = ref(window.location.hash)

  // Executa a ação quando realizar a navegação entre páginas. Obter o conteúdo a partir da cerquilha
  window.addEventListener('hashchange', () => {
    referenciaRota.value = window.location.hash
  });

  // Função responsável por exibir a página específica
  const currentView = computed(() => {
    return routes[referenciaRota.value.slice(1) || '/'] || PaginaErro
  })
</script>