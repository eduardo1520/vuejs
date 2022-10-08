<template>
    <main class="columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo}">
        <div class="column is-one-quarter">
            <BarraLateral @aoTemaAlterado="trocarTema" />
        </div>
        <div class="column is-three-quarter conteudo">
            <FormTarefa @aoSalvarTarefa="salvarTarefa" />
            <div class="lista">
                <TarefaLista v-for="(tarefa,index) in tarefas" :key="index" :tarefa="tarefa" />
                <BoxTexto  v-if="listaVazia">
                    Você não está muito produtivo hoje :(
                </BoxTexto>
            </div>
        </div>
    </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BarraLateral from './components/BarraLateral.vue'
import FormTarefa from './components/FormTarefa.vue'
import TarefaLista from './components/TarefaLista.vue'
import ITarefa from './interfaces/ITarefa'
import BoxTexto from './components/BoxTexto.vue'
export default defineComponent({
    name: 'App',
    components: {
        BarraLateral,
        FormTarefa,
        TarefaLista,
        BoxTexto
    },
    data() {
        return {
            tarefas: [] as ITarefa[],
            modoEscuroAtivo: false
        }
    },
    computed: {
        listaVazia(): boolean {
            return this.tarefas.length === 0
        }
    },
    methods: {
        salvarTarefa(tarefa: ITarefa) {
            this.tarefas.push(tarefa)
        },
        trocarTema(modoEscuroAtivo: boolean) {
            this.modoEscuroAtivo = modoEscuroAtivo
        }
    }
})
</script>

<style>
.lista {
    padding: 1.25rem
}

main {
    --bg-primario: #fff;
    --texto-primario: #000;
}

main.modo-escuro {
    --bg-primario: #2b2d42;
    --texto-primario: #ddd;
}

.conteudo {
    background-color: var(--bg-primario);
}

</style>
