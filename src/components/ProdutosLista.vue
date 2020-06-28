<template>
  <section class="produtos-container">
    <div v-for="produto in produtos" :key="produto.id">
      <img
        v-if="produto.fotos"
        :src="produto.fotos[0].src"
        :alt="produto.fotos[0].titulo"
      />
      <h2 class="titulo">{{ produto.nome }}</h2>
      <p class="descricao">{{ produto.descricao }}</p>
      <p clas="preco">{{ produto.preco }}</p>
    </div>
  </section>
</template>

<script>
import { api } from "@/services.js";
import { serialize } from '@/helpers.js';

export default {
  name: "ProdutosListar",

  data: () => ({
    produtos: null,
    produtosPorPagina: 9,
  }),

  computed: {
    url() {
      const query = serialize(this.$route.query);
      return `/produto?_limit=${this.produtosPorPagina}${query}`;
    }
  },

  created() {
    this.getProdutos();
  },

  watch: {
    url() {
      this.getProdutos()
    }
  },

  methods: {
    getProdutos() {
      api.get(this.url).then((response) => {
        this.produtos = response.data;
      });
    },
  },
};
</script>

<style></style>
