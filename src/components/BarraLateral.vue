<template>
    <header>
        <h1 :style="logoStyle">
            <img src="../assets/logo.svg" alt="Task Traker" />
        </h1>
        <button class="button" @click="alterarTema" :style="buttonStyle">
            {{ textoBotao }}
        </button>
    </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "BarraLateral",
    emits: ["aoTemaAlterado"],
    data() {
        return {
            modoEscuroAtivo: false,
            logoStyle: {
                backgroundColor: "#FFF",
                borderRadius: "10px",
                padding: "10px 17px",
                marginBottom: "15px",
            },
            buttonStyle: {
                width: "148px",
            },
        };
    },
    computed: {
        textoBotao() {
            if (this.modoEscuroAtivo) {
                return "Dark mode ON";
            }
            return "Dark mode OFF";
        },
    },
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo;
            this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
        },
    },
});
</script>

<style scoped>
header {
    padding: 1rem;
    background: #0d3b66;
    width: 100%;
    height: 100vh;
    text-align: center;
}
@media (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>
