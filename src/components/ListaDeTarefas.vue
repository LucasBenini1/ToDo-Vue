<script setup>
const props = defineProps(['tarefas'])
</script>

<template>
  <ul class="list-group mt-4">
    <li
      class="list-group-item"
      v-for="tarefa in tarefas"
      :key="tarefa.titulo"
    >
      <input
        v-model="tarefa.finalizada"
        :id="tarefa.titulo"
        type="checkbox"
      />
      <label
        :for="tarefa.titulo"
        :class="{ done: tarefa.finalizada }"
        class="ms-3"
      >
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
