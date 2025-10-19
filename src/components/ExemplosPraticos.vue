<!-- exemplo 1 - Interpolação -->
 <!-- <template>
    <h1>{{ mensagem }}</h1>
 </template>

<script setup>
    const mensagem = 'Hello World'
</script> -->

<!-- exemplo 2 - Reatividade-->
<!-- <script setup>
import {ref, reactive} from 'vue'

const contador = reactive ({count:0}) // Objeto Reativo 
const mensagem = ref('Hello World')

</script>

<template>
    <h1>{{ mensagem }}</h1>
    <p>Contador: {{ contador.count }}</p>   
</template> -->

<!--exemplo 3 - Options API-->
<!-- <template>
    <p>Nome: {{ nome }}, Idade: {{ idade }}</p>
</template>

<script>
    export default {
        data: function(){
            return {
                nome: "Paulo",
                idade: 24
            }
        }
    }
</script> -->

<!-- exemplo 4 - Composition API -->

<!-- <template>
    <p>Nome: {{ nome }}, Idade: {{ idade }}</p>
</template>

<script>
    export default {
        setup: function(){
            const nome = "Paulo";
            const idade = 24;

            return { nome, idade };
        }
    }
</script> -->

<!-- exemplo 5 - Eventos(v-on) -->

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

<!--exemplo 6 - One Way DataBinding(v-bind)-->
<!-- <script setup>
    import {ref} from 'vue'

    const link = ref('https://vuejs.org')
</script>

<template>
    <a v-bind:href="link">Site Vue</a>
</template> -->

<!--exemplo 7 - Two Way DataBinding(v-model)-->
<!-- 
<template>
    <input v-model="nome">
    <p>Ola, {{ nome }}</p>
</template>

<script setup>
    import {ref} from 'vue';
    const nome = ref('')
</script> -->

<!--exemplo 8 - Condicional(v-if/v-else)-->
<!-- <script setup>
import {ref} from 'vue';

const logado = ref(true)

</script>

<template>
    <p v-if="logado">Bem vindo!</p>
        <p v-else>Faça Login</p>
</template> -->

<!--exemplo 9 - Loop(v-for)-->

<!-- <script setup>
import {ref} from 'vue';

const lista = ref([
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

<!--exemplo 10 - Computed -->

<!-- <script setup>
import {ref, computed} from 'vue'

const nome = ref('')
const nomeMaisculo = computed(() => nome.value.toUpperCase())
</script>

<template>
    <input v-model="nome" placeholder="Digite o seu nome">
    <p>{{ nomeMaisculo }}</p>
</template> -->







