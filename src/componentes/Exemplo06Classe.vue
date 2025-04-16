<!-- SCRIPT -->
<script setup>
    //Variável
    let validacao = false;
</script>

<!-- CSS (css é a estilização, cor, fonte, tamanho, entre outros)-->
<style>
    /* Classe (para criar classe no css basta apenas colocar ponto e depois o nome da classe [.exemplo] */
    .ok{color: green}

    .falha{color: red;}
</style>

<!-- HTML -->
 <template>
    <!-- class está chamando a variável validação, se a validação for verdadeira, será ok, senão, será falha -->
    <p :class="validacao ? 'ok' : 'falha'">Utilizando a diretiva class</p>
 </template>