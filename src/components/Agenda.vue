<template>
  <div class="app">
    <label for="escolhaData">Escolha o dia: </label>
    <input type="date" :min=hoje id="escolhaData" v-model="dataSelecionada" class="data">

    <form @submit.prevent="adicionarTarefa()" class="formulario">
      <input v-model="novaTarefa" type="text" placeholder="Adicione a tarefa" required/>
      <button type="submit">Adicionar</button>
    </form>

    <h2>Tarefas para <span class="dataDestacada">{{ dataFormatada }}</span></h2> <!--SPAN É UM CONTAINER GENÉRICO USADO PARA AGRUPAR ELEMENTOS-->
    <ul class="listaTarefas">
      <li v-for="(tarefa, index) in tarefasDatas" :key="index">
        {{ tarefa}}
        <button @click="removeTarefa(index)">X</button>
      </li>
    </ul>

    <p v-if="tarefasDatas.length === 0">Nenhuma tarefa para este dia.</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
const hoje = ref(new Date(new Date().setHours(new Date().getHours() - 3)).toISOString().slice(0,10)); //FORMATADA PARA NOSSO FUSO BRASILEIRO

const dataSelecionada = ref(new Date(new Date().setHours(new Date().getHours() - 3)).toISOString().slice(0,10)); 

const novaTarefa = ref(''); // TEXTO DIGITADO DENTRO DO INPUT
const todasTarefas = ref({}); //VAI GUARDAR TODAS AS LISTAS DE TAREFAS, ORGANIZADAS POR DATA


//PRIMEIRO CRIAR A FUNÇÃO QUE SALVA AS TAREFAS
function salvarTarefas(){
  localStorage.setItem("tarefasPorData", JSON.stringify(todasTarefas.value)); //Serve para gravar um item no LocalStorage .setItem(chave, valor)
  // localStorage só aceita texto, objetos ou arrays precisam ser convertidos em JSON

  //EXEMPLO VISUAL 
  // tarefasPorData: {   
  //   "2025-10-22": ["Estudar Vue", "Ir para a faculdade"],  
  //   "2025-10-23": ["Fazer compras"]                  
  // }
}

//DEPOIS CRIAR A FUNÇÃO DE ADICIONAR A TAREFA
function adicionarTarefa() {
  if(!novaTarefa.value.trim()) return; //CASO ESTEJA VAZIA
  
  if(!todasTarefas.value[dataSelecionada.value]){ //CASO NÃO EXISTA UMA LISTA PARA ESSA DATA, CRIA UMA
    todasTarefas.value[dataSelecionada.value] = [];
  }
  todasTarefas.value[dataSelecionada.value].push(novaTarefa.value.trim()); //ADICIONA NO ARRAY A TAREFA NOVA
  novaTarefa.value = ""; //LIMPAR O CAMPO DO INPUT
  salvarTarefas(); 
}


const tarefasDatas = computed(()=>{ //RETORNA A LISTA DE TAREFA DA DATA QUE O USUÁRIO ESCOLHER
  return todasTarefas.value[dataSelecionada.value] || [];
});


function removeTarefa(index) { 
  todasTarefas.value[dataSelecionada.value].splice(index,1); //REMOVE APENAS UM ITEM COM O INDEX PASSADO POR PARAMETRO
  if(todasTarefas.value[dataSelecionada.value].length === 0){ // SERVE PARA LIMPAR O OBJETO, POIS NÃO FAZ SENTIDO GUARDAR UMA DATA NA MEMÓRIA SEM TAREFA
    delete todasTarefas.value[dataSelecionada.value];
  }
  salvarTarefas();
  // const remove = todasTarefas.value.find(t => t.id === tarefa.id);
  // todasTarefas.value.splice(remove, 1)
}


const dataFormatada = computed(() => {
  const data = new Date(hoje.value);
  data.setDate(data.getDate() + 1);
  return data.toLocaleDateString("pt-BR", {
    weekday: "long",
    year: "numeric",
    month: "long", 
    day: "numeric",
  });
});



function carregarTarefas(){ // ESSA FUNÇÃO É PARA CASO O USUÁRIO RECARREGUE A PÁGINA, AS TAREFAS IRÃO SER RESGATADAS
  const carregar = localStorage.getItem("tarefasPorData") // BUSCA OS DADOS
  if(carregar){
    todasTarefas.value = JSON.parse(carregar) // CONVERTE DE VOLTA PARA OBJETO
  }
}
carregarTarefas();





</script>


<style scoped>

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