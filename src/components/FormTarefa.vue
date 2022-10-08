<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja adicionar?" v-model="descricao" />
            </div>
            <div class="column">
                <TemporizadorTime @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TemporizadorTime from './TemporizadorTime.vue';
export default defineComponent({
    name: 'FormTarefa',
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorTime
    },
    data() {
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            })
            this.descricao = ''
        }
    }

})
</script>

<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario)
}
</style>