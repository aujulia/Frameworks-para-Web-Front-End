<script>
export default {
  name: 'ProductCard',
  props: {
    nome: { type: String, required: true },
    preco: { type: Number, required: true },
    imagem: { type: String, required: true },
    area: { type: String, required: true }
  },
  emits: ['adicionado'],
  methods: {
    adicionar() {
      this.$emit('adicionado'); // avisa o componente pai
    }
  }
};
</script>

<template>
  <article class="card-livro">
    <img :src="imagem" :alt="'Capa ilustrativa de ' + nome" />
    <p class="area">{{ area }}</p>
    <h3>{{ nome }}</h3>
    <p class="preco">R$ {{ preco.toFixed(2).replace('.', ',') }}</p>
    <button class="btn-comprar" type="button" @click="adicionar">Adicionar ao Carrinho</button>
  </article>
</template>
