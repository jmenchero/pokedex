<template>
  <div class="page">
    <div class="page--filter">
      <FilterBox @filter="filterPokemons" />
    </div>
    <div class="page--list">
      <Card
        v-for="(pokemon, index) in filteredPokemons"
        :key="index"
        :title="pokemon.name"
        :url="pokemon.url"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      allPokemons: [],
      filter: '',
    }
  },
  async fetch() {
    const response = await this.$axios.get(
      'https://pokeapi.co/api/v2/pokemon?limit=1500'
    )
    this.allPokemons = response.data.results
  },
  computed: {
    filteredPokemons() {
      if (this.filter && this.filter.length > 2) {
        return this.allPokemons.filter((pokemon) =>
          pokemon.name.toLowerCase().includes(this.filter.toLowerCase())
        )
      } else {
        return this.allPokemons
      }
    },
  },
  methods: {
    filterPokemons(filter) {
      this.filter = filter
    },
  },
}
</script>

<style>
body {
  background: #ffe62c;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  overflow-y: scroll;
  font-family: 'Roboto', sans-serif;
}

.page {
  max-width: 780px;
  margin: 0 auto;
}

.page--filter {
  position: sticky;
  width: auto;
  top: 15px;
  left: auto;
  height: 50px;
  margin: 10px;
}

.page--list {
  display: flex;
  flex-wrap: wrap;
  align-content: space-around;
}
</style>
