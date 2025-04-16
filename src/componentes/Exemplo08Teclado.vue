<!-- SCRIPT -->
<script setup>

    //Função de mensagem recebe o alerta
    function mensagem (params) {
        alert ('Executando função');
    }

</script>

<!-- HTML -->
<template>
<!-- o input chama a função mensagem sempre que a tecla enter for digitada no campo do input [pode-se trocae enter por qualquer outra tecla, o enter foi um exemplo] quando a função mensagem for chamada, o alerta será exibido -->
    <input type="text" @keyup.enter="mensagem">
</template>