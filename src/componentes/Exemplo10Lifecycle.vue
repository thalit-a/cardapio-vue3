<!-- Lifecycle: São ações que podem acontecer em três etapas de um componente:
 
- Antes da criação;
- Durabte a criação;
- Após a criação.
-->

<!-- SCRIPT -->
<script setup>

    //Importações (ref para variável reativa e onMounted para o Lifecycle na etapa Após a criação)
    import { onMounted, ref } from 'vue';

    //Variável de texto reativa (devido ao ref [ver explicação no ex.05])
    let texto = ref('Hello World!');

    //Lifecycle função onMounted e é preciso adicionar o arrow function para declarar a função. Arrow function: () => {}
    //setTimeout é um comando para efetuar uma ação após algum tempo, o timeout é definido em milisegundos, 3000 = 3s
    onMounted(() => {
        setTimeout(() => {
            texto.value = 'Alterando o texto!'
        }, 3000);

    });

</script>

<!-- HTML -->
 <template>
    <h1>{{ texto }}</h1>
 </template>