<template>
    <header>
        <h1 :style="logoStyle">
            <img src="../assets/logo.svg" alt="Task Traker" />
        </h1>
        <button class="button" @click="alterarTema" :style="buttonStyle">
            {{ textoBotao }}
        </button>
        <nav class="panel mt-5">
            <ul>
                <li>
                    <router-link to="/" class="link">
                        <i class="fas fa-tasks"></i>
                        tarefas
                    </router-link>
                </li>
                <li>
                    <router-link to="/projetos" class="link">
                        <i class="fas fa-project-diagram"></i>
                        projetos
                    </router-link>
                </li>
            </ul>
        </nav>
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
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo;
            this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
        },
    },
    computed: {
        textoBotao(): string {
            return this.modoEscuroAtivo ? 'Dark mode ON' : 'Dark mode OFF'
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

.panel li {
    margin: 8px 0;
}

.link {
    color: #fff;
}

.link:hover {
    color: #FAF0CA;
}

.link.router-link-active {
    color: #FAF0CA;
}</style>
