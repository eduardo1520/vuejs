<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTime :tempoEmSegundo="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
                    <span class="icon">
                    <i class="fas fa-play"></i>
                    </span>
                    <span>Play</span>
                </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
                    <span class="icon">
                    <i class="fas fa-stop"></i>
                    </span>
                    <span>Stop</span>
                </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import CronometroTime from './CronometroTime.vue';

export default defineComponent({
    name: 'TemporizadorTime',
    emits: [
        'aoTemporizadorFinalizado'
    ],
    components: {
        CronometroTime
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
});
</script>

<style scoped>

</style>