<!-- SCRIPT -->
<script setup>

    //Função para validar o formulário
    //dentro da função validaFormulario está passando o termo 'event' para que assim se chame a função 'preventDefault' para evitar que o usuário seja redirecionado para outra página
    function validaFormulario(event) {
        alert ('Formulário enviado!');

        event.preventDefault();
    }

</script>

<!-- HTML -->
<template>
<!-- para utilizar o submit chamando uma função precisa de 02 elementos 'form' e 'input type submit'-->
<!-- submit está chamando a função validaFormulario -->
<!-- a tag form tem um atributo chamado 'ACTION' que permite um redirecionameto, ou seja, após efetuar o submit(envio) o usuário é redirecionado para outra página, para se evitar essa ação padrão é utilizado o evento 'preventDefault' -->
    <form action="https://www.google.com" @submit="validaFormulario">
        <input type="submit" value="Enviar formulário">
    </form>
</template>
