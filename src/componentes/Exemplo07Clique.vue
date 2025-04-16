<!-- SCRIPT -->
<script setup>

    //Função (dentro do parênteses se passa o parâmetro, caso haja necessidade, nesse caso não foi passado parâmetro, então o parênteses está vazio)
    function mensagem (params) {
        alert('Trabalhando com eventos de clique!');
    }
</script>

<!-- HTML -->
<template>
    <button @click="mensagem">Clique aqui</button>
</template>
<!-- LEITURA: a função mensagem recebe o alerta, quando se clica no botão ele chama a função mensagem, assim exibindo o alerta -->