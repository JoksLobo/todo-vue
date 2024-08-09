<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    tarefas: [
      {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
  })
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
      Você possui 7 tarefas pendentes
    </p>
  </header>
<form>
  <div class="row">
    <div class="col">
      <input class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
    </div>
    <div class="col-md-2">
      <button type="submit" class="btn btn-primary">Cadastrar</button>
    </div>
    <div class="col-md-2">
      <select class="form-control">
        <option value="todas">Todas as tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
      </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefa in estado.tarefas">
    <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
    <label class="ms-3" :for="tarefa.titulo">
      {{tarefa.titulo}}
    </label>
  </li>
</ul>
</div>
</template>

<style scoped>

</style>
