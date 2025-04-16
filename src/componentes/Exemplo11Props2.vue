<!-- SCRIPT -->
<script setup>

    //Obter props (foi criada uma constante chamada props, e dentro dos parênteses com colchetes referenciar as propriedades criadas)
    const props = defineProps(['nome', 'idade', 'cidade', 'cidades', 'funcao'])

</script>

<!-- HTML -->
<template>
    <h1>Nome: {{ nome }}</h1>
    <h1>Idade: {{ idade }}</h1>
    <h1>Cidade: {{ cidade }}</h1>

<!-- para criar lista sempre se usa ul e li -->

    <ul>
        <li v-for="v of cidades"> {{ v }}</li>
    </ul>

    <button @click="funcao">Clique aqui</button>
</template>