<template>
    <div class="container">   
        
        
        <carregando :contador="contadorValue" />
         
        <erro :campoERRO="erroMSG" :camposucesso="okMSG"/>

         <div class="columns">
                <div class="column is-half field">
                    <div :class="{control: true, field: true, 'is-loading is-primary': carregar }">
                        <p class="control">
                            <input class="input is-primary is-loading" max="99999999" type="number" v-model="cep">
                        
                            <button class="button"  @click="click()">Pesquisar</button>
                        </p>
                        
                    </div>
 
                </div>
                
            </div>
       
       <campo :ativarColuna="campos" :logradouroValue="logradouro" :bairroValue="bairro" :cidadeValue="cidade" :estadoValue="estado"/>
            
            
    

    </div>

</template>
<script>
    import axios from 'axios'
    import carregando from './carregando.vue'
    import campo from './campos.vue'
    import erro from './erroMensagem.vue'

export default {
    components:{
        carregando,
        campo,
        erro
      
    },

    data(){
        return {
            cep : '',
            erro: false,
            bairro: '',
            logradouro: '',
            cidade: '',
            estado: '',
            carregar: false,
            erroMSG: undefined,
            okMSG: undefined,
            contadorValue: 0,
            campos: false,
       

        }
    },
  
    methods: {
            click(){
                this.erroMSG = undefined;
                 this.okMSG = undefined;
                 this.bairro = "";
                 this.logradouro ="";
                 this.cidade ="";
                 this.estado ="";
                 this.contadorValue = 0;
                 this.intervalo = null;
                 this.campos = false;
                

                if(this.cep == 0 || this.cep == undefined || this.cep.length != 8){
                    this.erroMSG = "Número do Cep Inválido";
            

                }else{
                    axios.get("http://viacep.com.br/ws/"+this.cep+"/json/").then(res=>{

                        
                         if(res.data.erro == true){
                             this.carregar = true;
                             this.erroMSG = "Cep não Encontrado"
                             this.carregar =false;

                        }
                        else{
                            this.carregar = true;
                            this.intervalo = setInterval(()=>{
                                this.contadorValue += 25
                            },150)
                       
                        
                           setTimeout(() => {
                                 
                                    this.campos = true;   
                                    this.okMSG = "Busca Realizada Com sucesso !!!"
                                    this.bairro = res.data.bairro
                                    this.logradouro = res.data.logradouro
                                    this.cidade = res.data.localidade

                                    axios.get("https://servicodados.ibge.gov.br/api/v1/localidades/estados/"+ res.data.uf).then(res=>{
                                    
                                        this.estado = res.data.nome;
                                        this.carregar=false;
                                        this.contadorValue = 0;
                                        

                                    });
                                    
                                     clearInterval(this.intervalo);

                                }, 1500);
                    
                        }
                        
                    
                    }).catch(err=>{
                        console.log(err);
                    
                    })
                }
            }
    },

}
</script>