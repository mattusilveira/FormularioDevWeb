<script setup>
import { reactive, ref } from 'vue'

const titulo = ref('Olá VueJs!')
const mostrarResultado = ref(false)

const categorias = [
  {
    Id: 1,
    nome: 'Eletrônicos'
  },
  {
    Id: 2,
    nome: 'Vestuário'
  },
  {
    Id: 3,
    nome: 'Brinquedos'
  },
  {
    Id: 4,
    nome: 'Móveis'
  },
]

const produto = reactive({
  nome: '',
  preco: 0,
  quantidade: 0,
  categorias: []
})

function formatarPreco(preco) {
  return `R$ ${preco.toFixed(2).replace('.', ',')}`
}

</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulário</h2>
      <input type="text" v-model="titulo" />
      <h3>Informar dados dos produtos</h3>
      <div class="row">
        <label for="">Nome:</label>
        <input type="text" v-model="produto.nome" />
      </div>
      <div class="row">
        <label for="">Preço (em reais):</label>
        <input type="text" v-model="produto.preco" />
      </div>
      <div class="row">
        <label for="">Quantidade:</label>
        <input type="text" v-model="produto.quantidade" />
      </div>
      <fieldset>
        <legend>Categorias</legend>
        <div class="items-checkbox">
          <template v-for="Categoria in categorias" :key="Categoria.id">
            <input type="checkbox" :value="Categoria.id" v-model="produto.categorias" /> {{ categoria.nome }}
          </template>
        </div>
      </fieldset>
      <button @click="mostrarResultado = mostrarResultado">Mostrar</button>
    </div>
    <div v-if="mostrarResultado" class="resultado">
      <h2>Dados do produto</h2>
      <p>Nome: {{ produto.nome }}</p>
      <p>Preço: {{ formatarPreco(produto.preco) }}</p>
      <p>Em estoque: {{ produto.quantidade }}</p>
      <p>Categorias: {{ produto.categorias }}</p>
      <p v-for="categoria_id in produto.categorias" :key="categoria">{{ buscarNome(categoria_id) }}</p>
      <p>{{ mostrarResultado }}</p>
    </div>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
}

.container {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 1rem;
}

.formulario,
.resultado {
  width: 45vw;
  min-height: 70vh;
  border-radius: 20px;
  padding: 20px;
}

.formulario {
  background-color: rgba(12, 44, 114, 0.753);
}

.formulario .row {
  flex-direction: column;
  width: 80%;
  margin: 1.3rem 0;
  display: flex;
  justify-content: space-between;
}

.formulario .items-checkbox {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
}

.resultado {
  background-color: rgba(24, 114, 141, 0.726);
}
</style>