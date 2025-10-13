<script setup>
  import { ref } from 'vue';

  let id = 0;

  const novaTarefa = ref(''); // variável para criar uma tarefa nova
  const todasTarefas = ref([
    {id: id++, text: 'Arrumar a cama'}
  ]); //array das tarefas

  function adicionarTarefa(){
    todasTarefas.value.push({id: id++, text:novaTarefa.value})
  }

  function removeTarefa(tarefa){
    const remove = todasTarefas.value.find(t=>t.id === tarefa.id);
    todasTarefas.value.splice(remove,1)
  }
</script>
<template>
  <h1>Lista de Tarefas📅</h1>
  <form @submit.prevent="adicionarTarefa()">
    <input v-model="novaTarefa" required placeholder="Adicione a tarefa">
    <button>Adicionar Tarefa</button>
  </form>
  <ul>
    <li v-for="tarefa in todasTarefas" :key="tarefa.id">
      {{ tarefa.text }}
      <button @click="removeTarefa(tarefa)">X</button>
    </li>
  </ul>
</template>

<style scoped>
</style>