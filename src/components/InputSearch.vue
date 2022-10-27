<template>
  <div class="search-container">
    <div class="input-container">
      <img src="../assets/lupas.png" alt="imagem de uma lupa" id="img-lupa" />
      <input
        type="text"
        name="search-input"
        v-model="name"
        placeholder="Digite o nome do Pokemon"
      />
    </div>
    <button @click="$emit('pesquisarPokemon', name)">pesquisar</button>
  </div>
</template>
<script>
export default {
  name: "InputSearch",

  data() {
    return {
      name: "",
    };
  },

  emits: ["pesquisarPokemon"],
};
</script>

<style scoped></style>
