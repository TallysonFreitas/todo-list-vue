<script setup>
import { reactive } from 'vue';


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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Voce possui {{getTarefasPendentes().length}} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="adicionarTarefa()" action="">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required class="form-control" type="text" placeholder="Digite aqui a descricao da tarefa">
      </div>
      <div class="col-1">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento=> estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
    {{ estado.filtro }}
  </form>
  <ul class="list-group mt-4" v-for="tarefa in getTarefasfiltradas()">
    <li class="list-group-item">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
      <label :class="{done:tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">{{ tarefa.titulo }}</label>
    </li>
  </ul>
  </div>
  
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
