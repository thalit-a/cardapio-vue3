<!-- HTML -->
<template>
    <h1 class="bg-orange-200 text-black-800 font-bold text-4xl text-center my-5"> Receitas </h1>
    <div class="grid grid-cols-5 overflow-x-hidden gap-5">
        <div v-for="receita, index in receitas" class="max-w-sm bg-white border border-gray-200 rounded-lg shadow-sm dark:bg-gray-800 dark:border-gray-700">
            <a href="#">
                <img class="rounded-t-lg" :src="receita.image" alt="Imagem da receita" />
            </a>
            <div class="p-5">
                <a href="#">
                    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
                        {{receita.name}}
                    </h5>
                </a>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Ingredientes: {{ receita.ingredients }}
                </p>

                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Instruções de preparo: {{ receita.instructions }}
                </p>

                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Dificuldade: {{ receita.difficulty }}
                </p>
            </div>
        </div>
    </div>


<!-- table é usado para criar a tabela em si; tr é usada para definir uma linha dentro da tabela; td é utilizada para definir uma célula dentro de uma linha, na horizontal; th utilizado para células de título -->
    <table border="1">
<!-- O [v] é um objeto, então em cada linha ele terá um valor diferente; as variáveis foram retirads da API na url-->
        <thead>
            <tr>
                <th>Id</th>
                <th>Nome</th>
                <th>Ingredientes</th>
                <th>Instruções</th>
                <th>Tempo de preparo</th>
                <th>Porções</th>
                <th>Dificuldade</th>
                <th>Calorias por porção</th>
                <th>Imagem</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="receita in receitas">
                <td> {{ receita.id }} </td>
                <td> {{ receita.name }} </td>
                <td> {{ receita.ingredients }} </td>
                <td> {{ receita.instructions }} </td>
                <td> {{ receita.prepTimeMinutes }} </td>
                <td> {{ receita.servings }} </td>
                <td> {{ receita.difficulty }} </td>
                <td> {{ receita.caloriesPerServing }} </td>
                <td>
<!-- receita.image irá mostrar apenas a url da imagem, o correto é usar a tag img, para que assim a imagem da url seja exibida;
o [alt] é um texto alternativo, para caso a imagem não carregue, será o texto exibido no lugar da imagem -->
                    <img :src="receita.image" alt="Imagem da receita" style="width: 100px; height: auto;"/>
                </td>
            </tr>
        </tbody>
    </table>

</template>

<!-- SCRIPT -->
<script setup>
    //Importações
    import { onMounted, ref } from 'vue';

    //Vetor contendo as postagens (vetor=array) variável vetor
    let vetor = ref ([]);
    let receitas = ref ([]);

    // onMounted é lifecycle, tem vários, o onMounted é quando é carregado; fetch é usado para fazer requisições, buscar ou enviar dados para servidor sem precisar recarregar a página.

    const fetchData = () => {
        fetch('https://dummyjson.com/recipes')
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Erro ao buscar os dados: ${response.status} - ${response.statusText}`);
                }
                return response.json();
            })
            .then(dados => {
                receitas.value = dados.recipes;
            })
            .catch(error => {
                console.error('Erro ao carregar as receitas:', error);
            });
    }

    onMounted(() => {
        fetchData();
    })
</script>