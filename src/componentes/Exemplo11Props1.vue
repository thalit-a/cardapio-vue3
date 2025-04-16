<!-- 
    PROPS -> Propriedades.
    
    A utilização da Props fornece uma comunicação entre componentes, podemos enviar ~
    informações estáticas, variáveis e funções
 -->

<!-- SCRIPT -->
<script setup>

    //Importar componente
    import Exemplo11Props2 from './Exemplo11Props2.vue';

    //Variáveis
    let cidade = 'Belo Horizonte';
    let cidades = ['Belo Horizonte', 'Rio de Janeiro', 'Curitiba', 'Ceará'];

    //Função
    function mensagem(){
        alert('Função criada no componente: Exemplo11Props1');
    }
</script>

<!-- HTML -->
<template>
<!-- propriedades chamadas nome e idade, propriedade é flexível, pode ser dado qualquer nome. Na variável cidade tem dois pontos na frente [:] porque para variáveis e funções, como são dinâmicas, se usa os dois pontos antes -->
    <Exemplo11Props2 nome="Ralf" idade="33" :cidade="cidade" :cidades="cidades" :funcao="mensagem"></Exemplo11Props2>
</template>