<template>
  <div class="page">
    <div class="page--filter"></div>
    <div class="page--list">
      <Card
        v-for="(pokemon, index) in pokemons"
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
      pokemons: [],
    }
  },
  async fetch() {
    const response = await this.$axios.get(
      'https://pokeapi.co/api/v2/pokemon?limit=50'
    )
    this.pokemons = response.data.results
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
