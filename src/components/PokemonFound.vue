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

<style scoped></style>
