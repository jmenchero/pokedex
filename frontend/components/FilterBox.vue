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
  display: flex;
  text-align: center;
  height: 100%;
  width: 100%;
  font-size: 20px;
  font-weight: 100;
  box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
  -moz-box-shadow: 0px 0px 10px 2px rgba(0, 0, 0, 0.2);
}

input,
input:focus {
  border: none;
  outline: none;
}
</style>
