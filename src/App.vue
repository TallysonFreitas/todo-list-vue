<script setup>
  import { reactive } from 'vue';
  import Cabecalho from '/components/cabecalho.vue';
  import Formulario from '/components/formulario.vue';
  import ListaDeTarefas from '/components/ListaDeTarefas.vue';

  const estado =reactive({
    filtro:'Todas',
    tarefaTemporaria:'',
    tarefas:[
      {
        titulo:'Estudar ES6',
        finalizada:false
      },
      {
        titulo:'Estudar Sass',
        finalizada:false
      },
      {
        titulo:'Ir para a academia',
        finalizada:true
      }
    ]
  })

const getTarefasPendentes = () =>{
  return estado.tarefas.filter(tarefa => tarefa.finalizada == false )
}
const getTarefasFinalizadas = () =>{
  return estado.tarefas.filter(tarefa => tarefa.finalizada == true )
}

const getTarefasfiltradas = () => {
  const { filtro } = estado;
  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

function adicionarTarefa() {  
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada:false,
  }

  estado.tarefas.push(tarefaNova)
  estado.tarefaTemporaria = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="adicionarTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefas="getTarefasfiltradas()"/>
    
  
  </div>
  
</template>

