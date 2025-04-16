<!-- SCRIPT -->
<script setup>

    //Importações
    import { onMounted, ref } from 'vue';

    //Vetor contendo as postagens (vetor=array) variável vetor
    let vetor = ref ([]);

    // onMounted é lifecycle; fetch é usado para fazer requisições, buscar ou enviar dados para servidor sem precisar recarregar a página.
    onMounted(() => {
        fetch('https://jsonplaceholder.typicode.com/posts')
    // depois que acessar a api da url acima, terá como retorno/promessa uma requisição, e essa requisição está sendo convertida em json para se ter acesso ao conteúdo; [.then] representa promessa
        .then(retorno => retorno.json())
    //retorno já convertido em json, passado para o vetor
        .then(retorno => vetor.value = retorno)
    })

</script>

<!-- HTML -->
<template>

    <h1> Requisições </h1>

<!-- table é usado para criar a tabela em si; tr é usada para definir uma linha dentro da tabela; td é utilizada para definir uma célula dentro de uma linha, na horizontal -->
    <table>
<!-- O [v] é um objeto, então em cada linha ele terá um valor diferente; userId, Id, title e body foram retirados da API na url-->
        <tr v-for="v in vetor">
            <td> {{ v.userId }}</td>
            <td> {{ v.id }}</td>
            <td> {{ v.title }}</td>
            <td> {{ v.body }}</td>
        </tr>
    </table>

</template>