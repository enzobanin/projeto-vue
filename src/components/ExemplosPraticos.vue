<!-- exemplo 1 - INTERPOLAÇÃO -->

<!-- <script setup>
import {ref} from 'vue'; sempre precisa importar o ref

const nome = ref('Julia');
const cargo = ref('Desenvolvedora');
</script>

<template>
    <p>{{ nome + cargo}}</p> da pra usar separado tb {{ nome }} é {{ cargo }}
</template> -->

<!--------------------------------------------------------------------------->

<!-- exemplo 2 - REATIVIDADE-->

<!-- <script setup>
import {ref, reactive} from 'vue'

const contador = reactive ({count:0}) // Objeto Reativo 
const mensagem = ref('Hello World')

</script>

<template>
    <h1>{{ mensagem }}</h1>
    <p>Contador: {{ contador.count }}</p>   
</template> -->

<!--------------------------------------------------------------------------->

<!-- exemplo 3 - OPTIONS API -->

<!-- <template>
    <h1>Utilizando Options API</h1>
    <p>{{ n1 }} + {{ n2 }} = {{ somar() }}</p>
</template>

<script>
export default {
    data() { // Dados do Componente - TEM QUE SEPARAR OS DADOS, DOS METODOS
        return {
            n1: 2,
            n2: 5
        }
    },

    methods: { // Métodos/"Funções" do Componente
        somar() {
            return this.n1 + this.n2; // É NECESSARIO O USO DO THIS PARA ACESSAR O VALOR DA VARIAVEL 
        }
    },

    mounted() { // O que será executado assim que for montado
        console.log("O componente para soma foi criado");
    }
}
</script> -->

<!--------------------------------------------------------------------------->

<!-- exemplo 4 - COMPOSITION API -->

<!-- <template>
    <h1>Utilizando Composition API Com Setup Direto</h1>
    <p>{{ n1 }} / {{ n2 }} = {{ dividir() }}</p>
</template>

<script setup> // Simplifica a criação do Componente
import { onMounted, ref } from 'vue';
const n1 = ref(2);
const n2 = ref(5);

function dividir() {
    return n1.value / n2.value;
}

onMounted (() => {
    console.log("O componente para divisão foi criado");
})
</script> -->

<!--------------------------------------------------------------------------->

<!-- exemplo 5 - EVENTOS(v-on) -->

<!-- <template>
    <button @click="aumentar" class="botao">
        <p>Contador: {{ contador }}</p>
    </button>
</template>

<script setup>
    import {ref} from 'vue'

    const contador = ref(0)

    function aumentar(){
        contador.value ++;
    }
</script> -->

<!--------------------------------------------------------------------------->

<!--exemplo 6 - ONE WAY DATABINDING(v-bind)-->

<!-- <script setup>
    import {ref} from 'vue'

    const link = ref('https://vuejs.org')
</script>

<template>
    <a v-bind:href="link">Documentação Vue</a>
</template> -->

<!--------------------------------------------------------------------------->

<!--exemplo 7 - TWO WAY DATABINDING(v-model)-->

<!-- <template>
    <input v-model="nome">
    <p>Ola, {{ nome }}</p>
</template>

<script setup>
    import {ref} from 'vue';
    const nome = ref('')
</script> -->

<!--------------------------------------------------------------------------->

<!--exemplo 8 - CONDICIONAL(v-if/v-else)-->

<!-- <script setup>
import {ref} from 'vue';

const logado = ref(true)

</script>

<template>
    <p v-if="logado">Bem vindo!</p>
        <p v-else>Faça Login</p>
</template> -->

<!--------------------------------------------------------------------------->

<!--exemplo 9 - LOOP(v-for)-->

<!-- <script setup>
import {ref} from 'vue';

const lista = ref([ criando um array com objetos
    {id: 1,nome: "João"},
    {id: 2,nome: "Anderson"},
    {id: 3,nome: "Livia"},
    {id: 4,nome: "Leticia"},
    ])
</script>

<template>
    <ul>
        <li v-for="item in lista" :key="item.id"> 
            {{ item.nome }}
        </li>
    </ul>
</template> -->

<!--------------------------------------------------------------------------->

<!--exemplo 10 - COMPUTED -->

<!-- <script setup>
import {ref, computed} from 'vue'

const nome = ref('')
const nomeMaisculo = computed(() => nome.value.toUpperCase()) função lambda ou Arrow Function
</script>

<template>
    <input v-model="nome" placeholder="Digite o seu nome">
    <p>{{ nomeMaisculo }}</p>
</template> -->







