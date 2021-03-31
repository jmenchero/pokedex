<template>
  <div>
    <Loading v-if="!loaded" />
    <div v-if="loaded" ref="page" class="page">
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
  </div>
</template>

<script>
import Loading from '../components/Loading.vue'
export default {
  components: { Loading },
  data() {
    return {
      allPokemons: [],
      filter: '',
      limit: 15,
      loaded: false,
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
        return this.allPokemons
          .filter((pokemon) =>
            pokemon.name.toLowerCase().includes(this.filter.toLowerCase())
          )
          .slice(0, this.limit)
      } else {
        return this.allPokemons.slice(0, this.limit)
      }
    },
  },
  mounted() {
    this.loadNextPokemons()
    this.changeBackgroundAfterLoading()
  },
  methods: {
    filterPokemons(filter) {
      this.limit = 15
      this.filter = filter
    },
    loadNextPokemons() {
      window.onscroll = function () {
        const alreadyDisplayedPixels =
          document.documentElement.scrollTop + window.innerHeight
        const noTriggerArea = this.$refs.page.offsetHeight - 300
        if (alreadyDisplayedPixels >= noTriggerArea) {
          this.limit += 5
        }
      }.bind(this)
    },
    changeBackgroundAfterLoading() {
      setTimeout(() => {
        document.body.style.backgroundColor = '#ffe62c'
        this.loaded = true
      }, 3000)
    },
  },
}
</script>

<style>
html {
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
  z-index: 1;
}

.page--list {
  display: flex;
  flex-wrap: wrap;
  align-content: space-around;
  justify-content: center;
  z-index: 0;
}
</style>
