<template>
  <section class="produtos-container">
    <div v-for="produto in produtos" :key="produto.id">
      <img v-if="produto.fotos" :src="produto.fotos[0].src" :alt="produto.fotos[0].titulo">
      <h2 class="titulo">{{produto.nome}}</h2>
      <p class="descricao">{{produto.descricao}}</p>
      <p clas="preco">{{produto.preco}}</p>
    </div>
  </section>

</template>

<script>

export default {
  name: 'ProdutosListar',

  data: () => ({
    produtos: null
  }),

  created() {
    this.getProdutos()
  },

  methods: {

    getProdutos() {
      fetch('http://localhost:3000/produto')
        .then(response => response.json())
        .then(response => { this.produtos = response})
    }
  }
}

</script>

<style>

</style>
