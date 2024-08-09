<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import listaDeTarefas from './components/listaDeTarefas.vue';

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
    <Cabecalho :tarefa-pendente="getTarefaPendente().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = estado.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <listaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


