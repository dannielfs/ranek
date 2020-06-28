<template>
  <form action="">
    <input name="busca" id="busca" v-model="busca" type="text">
    <input type="submit" id="lupa" value="Buscar" @click.prevent="buscarProdutos">
    {{busca}}
  </form>
</template>

<script>

export default {
  name: "ProdutosBuscar",
  data: () => ({
    busca: '',
  }),
  methods: {
    buscarProdutos() {
      this.$router.push({query: { q: this.busca }})
    }
  }

}

</script>

<style>

</style>
