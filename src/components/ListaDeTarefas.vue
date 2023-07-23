<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4" v-if="props.tarefas.length > 0" v-for="tarefa in props.tarefas">
        <li class="list-group-item">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label :class="{done:tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">{{ tarefa.titulo }}</label>
        </li>
    </ul>
    <h2 class="ms-5 mt-2" v-else>Nao existem tarefas pendentes</h2>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>
