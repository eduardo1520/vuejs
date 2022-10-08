<template>
    <div class="box has-text-weight-bold">
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroTime :tempoEmSegundo="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent, PropType } from "vue"
import CronometroTime from './CronometroTime.vue'

export default defineComponent({
    name: 'TarefaLista',
    components: {
        CronometroTime
    },
    props: {
        tarefa: {
            type: Object as PropType < ITarefa > ,
            required: true
        }
    }
});
</script>

<style scoped>
.box {
    background: #FAF0cA
}
</style>