<script setup>
import { reactive } from 'vue';

  const estado = reactive({//cria o estado das tarefas
    filtro:'todas',//cria o filtro para as tarefas(TOdas, finalazadas e pendentes)
    tarefaTemp: '',
    tarefas: [//cria o objeto das tarefas
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

  const getTarefaPendente = () => { //recupera a quantidade de tarefas pendentes e mostra no contador
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefaFinalizada = () => { //recupera a quantidade de tarefas finalizadas e mostra no contador
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {//recupera a quantidade de tarefas filtradas
    const {filtro} = estado;

    switch (filtro){
      case 'pendentes':
        return getTarefaPendente();
      case 'finalizadas':
        return getTarefaFinalizada();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {//recupera as tarefas cadastradas
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
      Você possui {{ getTarefaPendente().length }} tarefas pendentes
    </p>
  </header>
<form @submit.prevent="cadastraTarefa">
  <div class="row">
    <div class="col">
      <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
    </div>
    <div class="col-md-2">
      <button type="submit" class="btn btn-primary">Cadastrar</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
        <option value="todas">Todas as tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
      </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
    <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
    <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
      {{tarefa.titulo}}
    </label>
  </li>
</ul>
</div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
