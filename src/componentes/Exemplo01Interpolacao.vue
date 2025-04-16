<!-- SCRIPT -->
<script setup>

//Variáveis
let nome = 'Rebeca';
let idade = 31;
let numero1 = 20;
let numero2 = 10;

</script>

<!-- HTML (fica dentro do template, esse por sua vez é a área útil que o vue irá utilizar para manipular os elementos html)--> 
 <template>
    <p>{{ 'Olá ' + nome + ' você tem ' + idade + ' anos.' }}</p>
    <p>{{ numero1+numero2 }}</p>
 </template>