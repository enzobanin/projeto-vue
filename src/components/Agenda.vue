<template>
  <div class="app">
    <label for="escolhaData">Escolha o dia: </label>
    <input type="date" :min=hoje id="escolhaData" v-model="dataSelecionada" class="data">

    <form @submit.prevent="adicionarTarefa()" class="formulario">
      <input v-model="novaTarefa" type="text" placeholder="Adicione a tarefa" required/>
      
      <!-- parte de prioridades dividido em alta, media e baixa -->
      <select v-model="novaPrioridade" class="selecionarPrioridade">
        <option disabled value="">Selecione a prioridade</option>
        <option value="alta">🔴 Alta</option>
        <option value="media">🟠 Média</option>
        <option value="baixa">🟢 Baixa</option>
      </select> <!--adiciona esse select para a prioridade-->


      <button type="submit">Adicionar</button>
    </form>

    <h2>Tarefas para <span class="dataDestacada">{{ dataFormatada }}</span></h2>
    <ul class="listaTarefas">
      <!--add :class="tarefa.prioridade" no final da proxima linha-->
      <li v-for="(tarefa, index) in tarefasDatas" :key="index" :class="tarefa.prioridade">
        <!-- adicionar todo o span novo -->
         <input type="checkbox" v-model=tarefa.feito>
        <span>
          {{ tarefa.texto }}
          <small class="labelPrioridade">({{ tarefa.prioridade }})</small>
        </span>

        <button @click="removeTarefa(index)">X</button>
      </li>
    </ul>

    <p v-if="tarefasDatas.length === 0">Nenhuma tarefa para este dia.</p>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
const hoje = ref(new Date().toISOString().slice(0,10));
let id = 0;

const dataSelecionada = ref(new Date().toISOString().slice(0,10)); 
const novaTarefa = ref(''); // variável para criar uma tarefa nova
//ADD PARA PRIORIDADE FUNCIONAR
const novaPrioridade = ref('');
const feito = ref(false);
const todasTarefas = ref([
]); //array das tarefas
function carregarTarefas(){
  const salvar = localStorage.getItem("tarefasPorData")
  if(salvar){
    todasTarefas.value = JSON.parse(salvar)
  }
}

carregarTarefas();

const tarefasDatas = computed(()=>{
  return todasTarefas.value[dataSelecionada.value] || [];
});

const dataFormatada = computed(() => {
  const dataObj = new Date(dataSelecionada.value);
  dataObj.setDate(dataObj.getDate() + 1);
  return dataObj.toLocaleDateString("pt-BR", {
    weekday: "long",
    year: "numeric",
    month: "long", 
    day: "numeric",
  });
});

//refatorar toda a parte de adicionarTarefa()
function adicionarTarefa() {
  if(!novaTarefa.value.trim() || !novaPrioridade.value) return;

  //add esta const, relacionado ao obejto prioridade
  const todasTarefa = {
    texto: novaTarefa.value.trim(),
    prioridade: novaPrioridade.value,
    feito: novaTarefa.feito
  };

  if(!todasTarefas.value[dataSelecionada.value]){
    todasTarefas.value[dataSelecionada.value] = [];
  }
  todasTarefas.value[dataSelecionada.value].push(todasTarefa);
  //add texto e prioridade
  novaTarefa.value = '';
  novaPrioridade.value = '';
  salvarTarefas();
  // todasTarefas.value.push({ id: id++, text: novaTarefa.value })
}

function removeTarefa(index) {
  todasTarefas.value[dataSelecionada.value].splice(index,1);
  if(todasTarefas.value[dataSelecionada.value].length === 0){
    delete todasTarefas.value[dataSelecionada.value];
  }
  salvarTarefas();
  // const remove = todasTarefas.value.find(t => t.id === tarefa.id);
  // todasTarefas.value.splice(remove, 1)
}

function salvarTarefas(){
  localStorage.setItem("tarefasPorData", JSON.stringify(todasTarefas.value));
}
</script>


<style scoped>

/* Estilos para o seletor de prioridade ADD*/
.selecionarPrioridade {
  flex: 1 1 30%;
  padding: 0.6rem;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
}

/* Estilos para as prioridades ADD*/
.labelPrioridade {
  font-size: 0.9rem;
  color: #666;
  margin-left: 0.5rem;
}


.app {
  display: flex;
  flex-direction: column;
  width: 80%;
  max-width: 600px;
  margin: 3rem auto 6rem auto;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #fefefe;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 2rem;
  color: #333;
}


h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #2a9d8f;
}


label {
  font-weight: bold;
  margin-bottom: 0.5rem;
  display: block;
}


.data {
  font-size: 1.2rem;
  padding: 0.7rem;
  border: 2px solid #2a9d8f;
  border-radius: 8px;
  background-color: #e0f7f4;
  color: #222;
  width: 100%;
  margin-bottom: 1.5rem;
}


.data:hover {
  background-color: #c4f2ec;
  cursor: pointer;
}


.formulario {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}


input[type="text"] {
  flex: 1;
  padding: 0.6rem;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
}


button {
  padding: 0.6rem 1rem;
  font-size: 1rem;
  border: none;
  border-radius: 8px;
  background-color: #2a9d8f;
  color: white;
  transition: background-color 0.2s;
}


button:hover {
  background-color: #21867a;
}


.listaTarefas {
  list-style: none;
  padding: 0;
}


.listaTarefas li {
  background: #f0f0f0;
  margin-bottom: 0.7rem;
  padding: 0.6rem 0.8rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 6px;
}

.listaTarefas li.alta {
  border-left: 6px solid #e63946;
}


.listaTarefas li.media {
  border-left: 6px solid #f4a261;
}


.listaTarefas li.baixa {
  border-left: 6px solid #2a9d8f;
}


.listaTarefas li button {
  background-color: transparent;
  color: #e63946;
  font-size: 1.2rem;
  cursor: pointer;
}


.dataDestacada {
  color: #264653;
  font-weight: bold;
}

</style>