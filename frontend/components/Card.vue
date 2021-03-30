<template>
  <div class="holder">
    <div
      class="card"
      :class="{ 'card-fullscreen': fullscreen }"
      @click="fullscreen = !fullscreen"
    >
      <div class="card--picture">
        <span class="card--id">ID / {{ id }}</span>
        <img v-if="image" :src="image" :alt="title" />
      </div>
      <div class="card--meta">
        <p class="card--title">{{ title }}</p>
        <div class="tags">
          <div v-for="(type, index) in types" :key="index" class="tags--tag">
            {{ type.type.name }}
          </div>
        </div>
        <div v-if="evolves" class="highlight">
          <p class="highlight--header">Evoluciona de:</p>
          <p class="highlight--value">{{ evolves }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    url: String,
  },
  data() {
    return {
      image: null,
      id: 0,
      types: [],
      evolves: '',
      fullscreen: false,
    }
  },
  async fetch() {
    await this.loadCard()
  },
  watch: {
    url() {
      this.loadCard()
    },
  },
  methods: {
    async loadCard() {
      const pokemon = await this.$axios.get(this.url)
      this.image = pokemon.data.sprites.front_default
      this.id = pokemon.data.id
      this.types = pokemon.data.types
      const species = await this.$axios.get(pokemon.data.species.url)
      this.evolves = species.data.evolves_from_species.name
    },
  },
}
</script>

<style scoped>
.holder {
  height: 280px;
  width: 240px;
  margin: 10px;
}

.card {
  height: 100%;
  width: 100%;
  background: #ffffff;
  border: 1px solid #d5d6d6;
  box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
  -moz-box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
}

.card-fullscreen {
  position: fixed;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
}

.card--picture {
  height: 50%;
  width: 100%;
  background: #dfdfdf;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.card--id {
  position: absolute;
  left: 0;
  bottom: 0;
  background: #d1cdca;
  padding: 3px 10px;
  font-size: 13px;
  color: #60381d;
}

.card--meta {
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.card--title {
  font-size: 20px;
  font-weight: 500;
  text-transform: capitalize;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
}

.tags--tag {
  border: 1px solid #60381d;
  opacity: 0.5;
  border-radius: 5px;
  color: #60381d;
  font-size: 12px;
  text-transform: uppercase;
  padding: 2px;
  margin-right: 5px;
}

.highlight {
  margin-top: 6px;
  border-left: 4px solid #60381d;
  padding: 0 4px;
}

.highlight--header {
  color: #60381d;
  font-size: 15px;
}

.highlight--value {
  font-size: 22px;
  font-weight: 300;
}
</style>
