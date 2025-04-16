<!-- SCRIPT -->
<script setup>
    //Vetor (um array com início e fim, parte da posição zero)
    let nomes = ['Alice', 'Bruna', 'Caio', 'Daniel', 'Ellen'];
</script>

<!-- HTML (ul é uma estrutura de lista)--> 
 <template>
    <ul>
        <li v-for="nome in nomes"> {{ nome }} </li>
    </ul>
 </template>