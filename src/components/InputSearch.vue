<template>
  <div class="search-container">
    <div class="input-container">
      <img src="../assets/lupas.png" alt="imagem de uma lupa" id="img-lupa" />
      <input type="text" name="search-input" v-model="name" />
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

<style scoped>
.input-container {
  width: 100%;
  max-width: 350px;

  background-color: #d7d7d7;
  display: flex;
  align-items: center;
  height: 36px;
  border-radius: 5px;
}
.input-container:hover {
  outline: auto;
}
.input-container input {
  width: 100%;
  max-width: 300px;
  padding: 6px 5px;
  font-size: 16px;
  border: none;
  outline: none;
  color: #222;
  font-weight: bold;
  background-color: #d7d7d7;
}

#img-lupa {
  width: 30px;
  height: 30px;
  margin: 0 4px;
}

.search-container {
  display: flex;
  flex-direction: column;
  gap: 4px;
  justify-content: center;
  align-items: center;
  margin-top: 60px;
}
.search-container button {
  background-color: #4ea95c;
  color: #222;
  font-size: 18px;
  padding: 8px 16px;
  border-radius: 5px;
  font-weight: bolder;
  margin-top: 16px;
}

@media (min-width: 768px) {
  .search-container {
    flex-direction: row;
  }
  .search-container button {
    margin-top: 0;
  }
}
</style>
