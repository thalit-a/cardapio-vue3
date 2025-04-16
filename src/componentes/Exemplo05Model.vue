<!-- SCRIPT -->
<script setup>

    //Importar o REF para a variável ser reativa, ou seja, interpolar a informação que aparece no campo input
    import {ref} from 'vue';

    //Variável (ao invés de usar somente o apóstofro [''], para ser reativo se faz necessário o uso do ref antes do apóstrofo [ref ('')])
    let texto = ref('');

</script>

 <!-- HTML (o input tipo texto vai utilizar a diretiva v-model para criar vinculo entre o input e a variável texto)-->
<template>
    <input type="text" v-model="texto">
    <p>{{ texto }}</p>
</template>