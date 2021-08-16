<template>
       <div v-if="contador != 0">

                <div class="modal is-active">
                    <div class="modal-background"></div>
                    <div class="modal-card">
                        <header class="modal-card-head" style="padding: 10px 5px">
                        <p class="modal-card-title">Pesquisando, Por Favor Aguarde...</p>
                        </header>
                        <section class="modal-card-body" >
                            <progress class="progress is-success" :value="contador" max="100"></progress>
                        </section>
  
                    </div>
                </div>
                
        </div>
</template>
<script>
export default {
    props:{
        contador:Number
    }
}
</script>