<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-5-desktop is-6-widescreen" role="form"
                aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" id="selecioneTarefa" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
            </div>
            <div class="column is-2-desktop is-2-widescreen">
                <div class="select">
                    <select v-model="idProjeto" id="selectProjeto">
                        <option value="">Selecione o projeto</option>
                        <option :value="projeto.id" v-for="projeto in projetos" :key="projeto.id">
                            {{ projeto.nome }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="column is-5-desktop is-4-widescreen">
                <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent } from "vue";
import Temporizador from "./Temporizador.vue";
import { useStore } from 'vuex'
import { key } from '@/store'

export default defineComponent({
    name: "Formulário",
    emits: ["aoSalvarTarefa"],
    components: {
        Temporizador,
    },
    data() {
        return {
            descricao: "",
            idProjeto: ''
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            this.$emit("aoSalvarTarefa", {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao,
                projeto: this.projetos.find(proj => proj.id == this.idProjeto)
            });
            this.descricao = "";
        },
    },
    setup() {
        const store = useStore(key)
        return {
            projetos: computed(() => store.state.projetos)
        }
    }
});
</script>
<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>
