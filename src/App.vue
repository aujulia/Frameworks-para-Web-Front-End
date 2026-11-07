<script>
// O Vue altera automaticamente a tela quando "carrinho" e "textoBusca" mudam.
import ProductCard from './components/ProductCard.vue';

export default {
  name: 'App',
  components: { ProductCard },
  data() {
    return {
      carrinho: 0,
      textoBusca: '',
      livros: [
        { id: 1, nome: 'Introdução ao Direito', preco: 39.90, area: 'Fundamentos', imagem: '/img/introducao-direito.svg' },
        { id: 2, nome: 'Direito Constitucional Básico', preco: 54.90, area: 'Constitucional', imagem: '/img/constitucional.svg' },
        { id: 3, nome: 'Direito Civil para Iniciantes', preco: 49.90, area: 'Civil', imagem: '/img/civil.svg' },
        { id: 4, nome: 'Noções de Direito Penal', preco: 44.50, area: 'Penal', imagem: '/img/penal.svg' },
        { id: 5, nome: 'Direitos do Consumidor', preco: 35.00, area: 'Consumidor', imagem: '/img/consumidor.svg' },
        { id: 6, nome: 'Direito do Trabalho na Prática', preco: 42.00, area: 'Trabalho', imagem: '/img/trabalho.svg' }
      ]
    };
  },
  computed: {
    // "computed" faz a busca atualizar enquanto o usuário digita.
    livrosFiltrados() {
      const busca = this.textoBusca.trim().toLowerCase();
      return this.livros.filter(livro =>
        livro.nome.toLowerCase().includes(busca) || livro.area.toLowerCase().includes(busca)
      );
    }
  },
  methods: {
    adicionarItem() {
      this.carrinho += 1; // reatividade: sem atualizar a página manualmente
    }
  }
};
</script>

<template>
  <div class="container">
    <header>
      <div>
        <h1>Livraria Jurídica</h1>
        <p>Livros de Direito para começar a estudar</p>
      </div>
      <div class="carrinho" aria-live="polite">
        🛒 Itens no carrinho: <strong>{{ carrinho }}</strong>
      </div>
    </header>
    <main>
      <section class="apresentacao">
        <h2>Conheça nossos livros de Direito</h2>
        <p>Pesquise por título ou área do Direito e escolha os livros que deseja adicionar ao carrinho.</p>
      </section>
      <div class="busca">
        <label for="pesquisa">Pesquisar livros</label>
        <input id="pesquisa" type="search" v-model="textoBusca"
          placeholder="Ex.: Direito Civil, Penal, Consumidor..." autocomplete="off" />
      </div>
      <p class="quantidade">Livros encontrados: {{ livrosFiltrados.length }}</p>
      <div class="livros-grid">
        <ProductCard v-for="livro in livrosFiltrados" :key="livro.id"
          :nome="livro.nome" :preco="livro.preco" :imagem="livro.imagem" :area="livro.area"
          @adicionado="adicionarItem" />
      </div>
      <p class="nenhum" v-if="livrosFiltrados.length === 0">Nenhum livro encontrado. Tente outro nome.</p>
    </main>
    <footer class="rodape">Trabakho Prático Julia Rodrigues Marques</footer>
  </div>
</template>
