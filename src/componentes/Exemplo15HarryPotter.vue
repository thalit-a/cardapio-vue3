<!-- HTML -->
<template>
    <h1 class="fonte-sans bg-orange-900 text-black-800 font-bold text-4xl text-center my-5"> Harry Potter: Personagens </h1>
    <div class="grid grid-cols-5 overflow-x-hidden gap-5">
        <div v-for="personagem in personagem" class="max-w-sm bg-white border border-gray-200 rounded-lg shadow-sm dark:bg-gray-800 dark:border-gray-700">
            <a href="#">
                <img class="rounded-t-lg" :src="personagem.image" alt="Imagem da personagem" />
            </a>
            <div class="p-5">
                <a href="#">
                    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
                        {{personagem.name}}
                    </h5>
                </a>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Casa de Hogwarts: {{ personagem.house }}
                </p>

                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Data de Nascimento: {{ personagem.dateOfBirth }}
                </p>

                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                   Espécie: {{ personagem.species }}
                </p>
            </div>
        </div>
    </div>
</template>

<!-- SCRIPT -->
<script setup>
    //Importações
    import { onMounted, ref } from 'vue';

    //Vetor contendo as postagens (vetor=array) variável vetor
    let personagem = ref ([]);

    // onMounted é lifecycle, tem vários, o onMounted é quando é carregado; fetch é usado para fazer requisições, buscar ou enviar dados para servidor sem precisar recarregar a página.
    const fetchData = () => {
        fetch('https://hp-api.onrender.com/api/characters')
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Erro ao buscar os dados: ${response.status} - ${response.statusText}`);
                }
                return response.json();
            })
            .then(dados => {
                personagem.value = dados;
            })
            .catch(error => {
                console.error('Erro ao carregar as personagens:', error);
            });
    }

    onMounted(() => {
        fetchData();
    })
</script>