<template>
  <section class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos"/>
    <Botao @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
    <Botao @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
  </section>
</template>


<script lang="ts">
import { defineComponent }  from 'vue';
import Cronometro from './Cronometro.vue'
import Botao from './Botao.vue'

export default defineComponent({
    name: 'TemporizadorTracker',
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro,
        Botao
    },
    data () {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar () {
            // quando iniciar o cronometro
            this.cronometroRodando = true
            // começar a contagem
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1    
            }, 1000)
        },
        finalizar () {
            // quando finalizar o cronometro
            this.cronometroRodando = false
            // limpar cronometro
            clearInterval(this.cronometro)
            // emitir evento quando o usuário der stop
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>

<style scoped>

</style>