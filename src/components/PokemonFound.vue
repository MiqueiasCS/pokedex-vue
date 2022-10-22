<template>
  <div class="pokemonFound-Container">
    <div class="pokemon-data">
      <div class="image">
        <p class="titles">Pokemon: {{ pokemonName }}</p>
        <div class="image-container">
          <img :src="pokemonImage" alt="imagem do pokemon" />
        </div>
      </div>
      <div class="details" v-if="showInfo">
        <p class="titles">Informações:</p>
        <div class="details-stats">
          <p v-for="(item, index) in stats" :key="index">
            <span>{{ item.stat.name }}</span> - {{ item.base_stat }}
          </p>
        </div>
      </div>
    </div>

    <hr />

    <div class="evolucoes" v-if="showInfo">
      <p class="titles">Evoluções:</p>
      <ul>
        <Evolutions
          v-for="(pokemon, index) in evolucoes"
          :key="index"
          :pokemon="pokemon"
          @click="$emit('pesquisarPokemon', pokemon.name)"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import Evolutions from "./Evolutions.vue";
export default {
  name: "PokemonFound",
  data() {
    return {
      evolImages: "../../public/img/quemeh.png",
    };
  },
  props: {
    pokemonImage: String,
    pokemonName: String,
    evolucoes: Array,
    stats: Array,
    showInfo: Boolean,
  },

  emits: ["pesquisarPokemon"],

  components: { Evolutions },
};
</script>

<style scoped>
.pokemonFound-Container {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.pokemon-data {
  display: flex;
  flex-direction: column;
}
.image-container {
  background-color: #222;
  width: 250px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
}

.image-container img {
  width: 100%;
}

.titles {
  font-size: 28px;
  color: #222;
  font-weight: bold;
  margin: 12px 0;
  text-align: center;
}

.details-stats p {
  background-color: #f8e9b3;
  padding: 7px 20px;
  margin-bottom: 5px;
  border-radius: 16px;

  font-size: 20px;
  color: #222;
}

.details-stats p span {
  font-weight: bold;
}

.details-stats p:hover {
  background-color: #f39444;
}

hr {
  background-color: black;
  height: 4px;
  width: 100%;
  border: none;
  border-radius: 50px;
  margin: 24px 0;
}
.evolucoes {
  width: 100%;
  margin-top: 8px;
  align-self: self-start;
}
.evolucoes .titles {
  text-align: center;
}

.evolucoes ul {
  list-style: none;
}

.evolucoes ul li {
  margin-bottom: 12px;
}

@media (min-width: 768px) {
  .pokemonFound-Container {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
    margin-top: 30px;
  }

  .pokemon-data[data-v-86b9007d] {
    flex-direction: row;
    gap: 16px;
    align-items: center;
  }

  .evolucoes {
    align-self: auto;
  }
}
</style>
