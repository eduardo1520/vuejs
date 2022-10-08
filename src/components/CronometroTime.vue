<template>
    <section>
        <strong class="display">{{ tempoDecorrido }}</strong>
    </section>
</template>

<script lang="ts">
import { defineComponent } from "vue"
export default defineComponent({
    name: 'CronometroTime',
    props: {
        tempoEmSegundo: {
            type: Number,
            default: 0
        }
    },

    computed: {
        tempoDecorrido(): string {
            let data = this.tempoMilissegundos()
            return new Date(data).toISOString().slice(11, 19)
        }
    },
    methods: {
        tempoMilissegundos(): number {
            return this.tempoEmSegundo * 1000
        }
    }
});
</script>

<style>
.display {
    color: var(--texto-primario);
}

</style>