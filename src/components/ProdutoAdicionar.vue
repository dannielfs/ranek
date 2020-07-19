<template>
  <form class="adicionar-produto">
    <label for="nome">Nome</label>
    <input type="text" id="nome" name="nome" v-model="produto.nome">
    <label for="preco">Preco (R$)</label>
    <input type="text" id="preco" name="preco" v-model="produto.preco">
    <label for="fotos">Fotos</label>
    <input type="file" id="fotos" name="fotos" ref="fotos">
    <label for="descricao">Descricao</label>
    <textarea id="descricao" name="descricao" v-model="produto.descricao"></textarea>
    <input class="btn" type="button" value="Adicionar Produto" @click.prevent="adicionarProduto">
  </form>
</template>

<script>
import { api } from '@/services.js'
export default {
  name: "ProdutoAdicionar",
  data: () => ({
    produto: {
      nome: '',
      preco: '',
      descricao: '',
      fotos: null
    }
  }),
  methods: {
    formatarProduto() {
      this.produto.usuario_id = this.$store.state.usuario.id;
    },
    adicionarProduto() {
      this.formatarProduto();
      api.post('/produto', this.produto).then(
        (response) => this.$store.dispatch('getUsuarioProdutos')
      ).catch( err => console.log(err))
    }
  }
};
</script>

<style scoped>
  .adicionar-produto {
    display: grid;
    grid-template-columns: 100px 1fr;
    align-items: center;
    margin-bottom: 60px;
  }

  .btn {
    grid-column: 2;
  }
</style>
