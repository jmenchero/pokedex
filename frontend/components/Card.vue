<template>
  <transition name="fade-in">
    <div class="holder">
      <div
        class="card"
        :class="{ 'card-fullscreen': open }"
        @click="$emit('toggle', 'hello')"
      >
        <div class="card--picture">
          <span class="card--id">ID / {{ id }}</span>
          <img
            v-if="displayedSprites.length === 0"
            class="card--loading"
            src="@/assets/png/poke-ball.png"
            :alt="title"
          />
          <img
            v-for="(sprite, index) in displayedSprites"
            :key="index"
            :src="sprite"
          />
        </div>
        <div class="card--meta">
          <p class="card--title">{{ title }}</p>
          <div class="tags">
            <div v-for="(type, index) in types" :key="index" class="tags--tag">
              {{ type.type.name }}
            </div>
          </div>
          <transition name="fade-in-right">
            <div v-if="evolves" class="highlight">
              <p class="highlight--header">Evoluciona de:</p>
              <p class="highlight--value">{{ evolves }}</p>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: '',
    },
    url: {
      type: String,
      default: '',
    },
    open: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      id: 0,
      types: [],
      sprites: [],
      evolves: undefined,
    }
  },
  async fetch() {
    await this.loadCard()
  },
  computed: {
    displayedSprites() {
      if (this.open) {
        return this.sprites.slice(0, 3)
      } else {
        return this.sprites.slice(0, 1)
      }
    },
  },
  watch: {
    url() {
      this.loadCard()
    },
  },
  methods: {
    async loadCard() {
      const pokemon = await this.$axios.get(this.url)
      this.sprites = this.getAllSprites(pokemon.data.sprites)
      this.id = pokemon.data.id
      this.types = pokemon.data.types
      const species = await this.$axios.get(pokemon.data.species?.url)
      this.evolves = species.data.evolves_from_species?.name
    },
    getAllSprites(sprites) {
      const allSprites = []
      allSprites.push(sprites.front_default)
      allSprites.push(sprites.back_default)
      allSprites.push(sprites.front_female)
      allSprites.push(sprites.back_female)
      allSprites.push(sprites.front_shiny)
      allSprites.push(sprites.back_shiny)
      allSprites.push(sprites.front_shiny_female)
      allSprites.push(sprites.back_shiny_female)
      allSprites.push(sprites.back_shiny_female)
      allSprites.push(sprites.dream_world?.front_default)
      allSprites.push(sprites.dream_world?.front_female)
      allSprites.push(sprites?.['official-artwork']?.front_default)
      const definedSprites = allSprites.filter(
        (_) => ![undefined, null].includes(_)
      )
      return definedSprites
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
  cursor: pointer;
  transition-duration: 0.1s;
}

.card:not(.card-fullscreen):hover {
  transform: scale(1.02);
  color: #60381d;
}

.card-fullscreen {
  position: absolute;
  height: 100vh;
  width: 100%;
  left: 0;
  top: 0;
  z-index: 100;
}

.card-fullscreen:hover {
  cursor: default;
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

.card--loading {
  animation: shake 0.82s infinite cubic-bezier(0.36, 0.07, 0.19, 0.97) forwards;
  transform: translate3d(0, 0, 0);
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

.fade-in-enter-active {
  animation: fadeIn 0.2s cubic-bezier(0.36, 0.07, 0.19, 0.97) forwards;
}

.fade-in-leave-active {
  animation: fadeIn 0.2s cubic-bezier(0.36, 0.07, 0.19, 0.97) reverse;
}

.fade-in-right-enter-active {
  animation: fadeInRight 0.5s cubic-bezier(0.36, 0.07, 0.19, 0.97) forwards;
}

.fade-in-right-leave-active {
  animation: fadeInRight 0.5s cubic-bezier(0.36, 0.07, 0.19, 0.97) reverse;
}
</style>
