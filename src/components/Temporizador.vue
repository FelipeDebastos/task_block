<template>
    <div class="column">
                <div class="is-flex is-align-items-center is-justify-content-space-between">
                    <Cronometro :tempoEmSegundos="tempoEmSegundos"/>
                    <BotaoTemporizador @click="iniciar" icone="fas fa-play" texto="Start" :desabilitado="cronometroAtivo"/>
                    <BotaoTemporizador @click="finalizar" icone="fas fa-stop" texto="Stop" :desabilitado="!cronometroAtivo"/>
                </div>
            </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue';
import BotaoTemporizador from './BotaoTemporizador.vue';

export default defineComponent({
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Temporizador',
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro, BotaoTemporizador
    },
    data() {
        return {
            tempoEmSegundos: 0,
            intervalo: 0,
            cronometroAtivo: false
        }
    },

    methods: {
        iniciar() {
            // 1 seg = 1000 ms
            this.intervalo = setInterval(() => {
                this.cronometroAtivo = true;
                this.tempoEmSegundos++;
            }, 1000)
        },
        finalizar() {
            this.cronometroAtivo = false;
            clearInterval(this.intervalo);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
            this.tempoEmSegundos = 0
        }
    }
})
</script>