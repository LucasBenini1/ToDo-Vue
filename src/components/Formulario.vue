<script setup>
const emit = defineEmits(['cadastrar', 'filtrar'])
const modelValue = defineModel()
</script>

<template>
  <form @submit.prevent="emit('cadastrar')">
    <div class="row">
      <div class="col">
        <input
          v-model="modelValue"
          required
          type="text"
          placeholder="Digite aqui a descrição da tarefa."
          class="form-control"
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select
          class="form-control"
          @change="evento => emit('filtrar', evento.target.value)"
        >
          <option value="todas">Todas Tarefas</option>
          <option value="pendentes">Tarefas Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
