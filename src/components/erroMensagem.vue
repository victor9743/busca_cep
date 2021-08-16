<template>
    <div>
        <article class="message is-danger" v-if="campoERRO != undefined">
            <div class="message-body">
                        <p>{{ campoERRO }}</p>
            </div>
        </article>

        <article class="message is-success" v-else-if="camposucesso != undefined">
            <div class="message-body">
                     <p>{{ camposucesso }}</p>
            </div>
        </article>
        
    </div>
 

    
</template>
<script>
export default {
    props:{
        campoERRO: String,
        camposucesso: String
    }
}
</script>