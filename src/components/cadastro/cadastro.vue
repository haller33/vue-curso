<template>

    <div>
        <h1 class="centralizado">Cadastro</h1>
        <h2 class="centralizado">{{ foto.titulo }}</h2>

        <form @submit.prevent="grava()">
            <div class="controle">
                <label for="titulo">TITULO</label>
                <input id="titulo" autocomplete="off"
                    v-model.lazy="foto.titulo">
            </div>

            <div class="controle">
                <label for="url">URL</label>
                <input id="url" autocomplete="off" 
                    v-model.lazy="foto.url">
                <imagem-responsiva v-show="foto.titulo" :url="foto.url" :titulo="foto.titulo"/>
            </div>

            <div class="controle">
                <label for="descricao">DESCRICAO</label>
                <textarea id="descricao" autocomplete="off" 
                    v-model="foto.descricao">
                </textarea>
            </div>

            <div class="centralizado">
                <meu-botao rotulo="GRAVAR" tipo="submit"></meu-botao>
                <router-link to="/">
                <meu-botao rotulo="VOLTAR" tipo="button"></meu-botao>
                </router-link><a/>
            </div>

        </form>
    </div>
    
</template>

<script>

import ImagemResponsiva from '../shared/imagem-responsiva/imagem-responsiva.vue'
import Botao from '../shared/botao/botao.vue'
import Foto from '../../domain/foto/foto.js'

export default {
    
    components: {

        'imagem-responsiva': ImagemResponsiva,
        'meu-botao': Botao
    }, 
    data (  ) {

        return {

            foto: new Foto ()
        }
    },
    methods: {

        grava() {

            this.resource
                .save( this.foto )
                .then( res => {
                    this.foto = new Foto ()
                }, err => console.log(
                    new Error ('erro in '+this.foto)
                ))
        }
    }, 
    created() {
        
        this.resource = this.$resource(`v1/fotos{/id}`)

    }
}
</script>

<style scoped>

.centralizado {

    text-align: center;
}

.controle {
    font-size: 1.2em;
    margin-bottom: 20px;
}
 
.controle label {
    display: block;
    font-weight: bold;
}

.controle label + input, .controle textarea {
    width: 100%;
    font-size: inherit;
    border-radius: 5px;
}

</style>
