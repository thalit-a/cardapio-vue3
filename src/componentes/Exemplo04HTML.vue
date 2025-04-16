<!-- SCRIPT -->
<script setup>
    //Variável (o v-html não só imprime o texto no navegador, ele imprime uma estrutura html, ou seja, além do texto ele pode conter parágrafo, cor, fonte, entre outros. Enquanto a interpolação faz apenas a impressão do texto, como se vê no exemplo)
    let texto = '<p style="color:red">Aprendendo a diretiva v-html</p>';
</script>

 <!-- HTML -->
  <template>
    <div v-html="texto"></div>
    
    <div> {{ texto }}</div>
  </template>