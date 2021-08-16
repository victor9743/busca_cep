<template>
         <div class="columns" v-if="ativarColuna != false">
                
                <div class="column is-half container">
                    <label for="">Endereço</label>
                    <input class="input is-primary" type="text" :value="logradouroValue" disabled>

                     <label for="">Bairro</label>
                    <input class="input is-primary" type="text" :value="bairroValue" disabled>

                     <label for="">Cidade</label>
                    <input class="input is-primary" type="text" :value="cidadeValue" disabled>
                     
                     <label for="">Estado</label>
                    <input class="input is-primary" type="text" :value="estadoValue" disabled>

                </div>

            </div>
</template>
<script>
export default {
    props:{
        ativarColuna: Boolean,
        logradouroValue: String,
        bairroValue: String,
        cidadeValue: String,
        estadoValue: String

    }
}
</script>