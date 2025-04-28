<script setup>
import { reactive } from "vue";
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: "",
  tarefas: [
    { titulo: "Estudar ES6", finalizada: false },
    { titulo: "Estudar SASS", finalizada: false },
    { titulo: "Estudar LESS", finalizada: true }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <!-- Corrigido: passando o valor dinâmico corretamente -->
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario 
      v-model="estado.tarefaTemp"
      @cadastrar="cadastraTarefa"
      @filtrar="filtro => estado.filtro = filtro"
    />
    <ListaDeTarefas 
      :tarefas="getTarefasFiltradas()"
    />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
