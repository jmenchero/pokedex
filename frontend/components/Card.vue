<template>
  <div class="holder">
    <div
      class="card"
      :class="{ 'card-fullscreen': fullscreen }"
      @click="fullscreen = !fullscreen"
    >
      <div class="card--picture">
        <img v-if="image" :src="image" :alt="title" />
      </div>
      <div class="card--meta">
        <p class="card--title">{{ title }}</p>
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
      fullscreen: false,
    }
  },
  async fetch() {
    const response = await this.$axios.get(this.url)
    this.image = response.data.sprites.front_default
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
  border: 1px solid #eaebeb;
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
}

.card--meta {
  padding: 20px;
}

.card--title {
  font-size: 20px;
  font-weight: 500;
}
</style>
