<template>
  <input
    v-model="filter"
    class="filter"
    type="text"
    placeholder="Filtra pokemons por nombre..."
    @keyup="$emit('filter', filter)"
  />
</template>

<script>
export default {
  data() {
    return {
      filter: '',
    }
  },
}
</script>

<style scoped>
.filter {
  background: #ffffff;
  border: 1px solid #eaebeb;
  display: flex;
  text-align: center;
  height: 100%;
  width: 100%;
  font-size: 20px;
  font-weight: 100;
}
</style>
