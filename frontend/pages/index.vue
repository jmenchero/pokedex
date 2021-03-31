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
          :open="pokemon.open"
          @toggle="toggleCard(pokemon)"
        />
      </div>
    </div>
  </div>
</template>

<script>
function noScroll() {
  window.scrollTo(0, 0)
}

export default {
  data() {
    return {
      allPokemons: [],
      filter: '',
      limit: 15,
      loaded: false,
      previousScroll: undefined,
    }
  },
  async fetch() {
    const response = await this.$axios.get(
      'https://pokeapi.co/api/v2/pokemon?limit=1500'
    )
    response.data.results.forEach((_) => (_.open = false))
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
  async mounted() {
    if (window.location.href.includes('pokemons')) {
      await this.$fetch()
      this.loaded = true
      const name = window.location.href.substring(
        window.location.href.lastIndexOf('/') + 1
      )
      const pokemon = this.allPokemons.find(
        (_) => _.name.localeCompare(name) === 0
      )
      this.filteredPokemons.push(pokemon)
      this.toggleCard(pokemon)
    }
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
    toggleCard(pokemon) {
      pokemon.open = !pokemon.open
      if (this.previousScroll === undefined) {
        if (!window.location.href.includes('pokemons')) {
          history.pushState(
            {},
            null,
            window.location.href + 'pokemons/' + pokemon.name
          )
        }
        this.previousScroll = document.documentElement.scrollTop
        window.addEventListener('scroll', noScroll, true)
        window.scrollTo(0, 0)
      } else {
        history.pushState(
          {},
          null,
          window.location.protocol + '//' + window.location.host
        )
        window.removeEventListener('scroll', noScroll, true)
        window.scrollTo(0, this.previousScroll)
        this.previousScroll = undefined
      }
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
  padding-top: 0;
  margin-top: 0;
}

body {
  height: 100%;
  width: 100%;
  padding: 0;
  margin: 0;
}

.page {
  max-width: 780px;
  position: relative;
  margin: 0 auto;
}

.page--filter {
  position: sticky;
  width: auto;
  top: 15px;
  left: auto;
  height: 50px;
  margin: 0 10px;
  z-index: 1;
}

.page--list {
  display: flex;
  flex-wrap: wrap;
  align-content: space-around;
  justify-content: center;
  margin-top: 30px;
  z-index: 0;
}
</style>
