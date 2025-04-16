<template>
    <div>
        <h1> Isso aqui vai dentro de cardápio</h1>
        <p>Total: R$ {{ total.toFixed(2) }}</p>
        <div>
            <!-- Passando as props para o componente filho EmiteEvento -->
            <EmiteEvento :name="item.name" :prepTimeMinutes="item.prepTimeMinutes" :imagem="item.image" @foiAdicionado="atualizarTotal"/>
        </div>

        <div v-if="tela === 'detalhes'">
            <h2>{{ produto.nome }}</h2>
            <p>{{ produto.descricao }}</p>
            <img :src="produto.imagem" alt="Imagem do prato" />
            <p>Preço: R${{ produto.preco.toFixed(2) }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import EmiteEvento from './EmiteEvento.vue';

// Variáveis reativas
const total = ref(0); // Total do carrinho
const tela = ref(''); // Controle da tela atual
const produto = ref({}); // Detalhes do prato selecionado
const receitas = ref({}); // Dados de receitas agrupadas por tipo de culinária
const item = ref({}); // Item do prato que será adicionado

// Função para atualizar o total com base no valor recebido
function atualizarTotal(produto) {
  total.value += produto.valor;
}

// Função para buscar os dados das receitas da API
const fetchData = () => {
    fetch('https://dummyjson.com/recipes')
        .then(response => {
            if (!response.ok) {
                throw new Error(`Erro ao buscar os dados: ${response.status} - ${response.statusText}`);
            }
            return response.json();
        })
        .then(dados => {
            const resultado = {};
            dados.recipes.forEach(recipe => {
                if (resultado[recipe.cuisine]) {
                    resultado[recipe.cuisine].push(recipe);
                } else {
                    resultado[recipe.cuisine] = [recipe];
                }
            });

            receitas.value = resultado; // Atualiza as receitas com a estrutura organizada

            item.value = {
                name: dados.recipes[0].name,
                prepTimeMinutes: dados.recipes[0].prepTimeMinutes,
                image: dados.recipes[0].image
            };
        })
        .catch(error => {
            console.error('Erro ao carregar as receitas:', error);
        });
}

// Função para abrir detalhes do prato
const abrirDetalhes = (receita) => {
    tela.value = 'detalhes'; 
    produto.value = {
        nome: receita.name,
        descricao: receita.ingredients,
        imagem: receita.image,
        preco: receita.prepTimeMinutes,
        categoria: receita.cuisine
    };
};

onMounted(() => {
    fetchData(); // Faz a requisição à API para carregar as receitas
});
</script>
