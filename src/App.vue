<template>
  <main>
    <section class="search-pokemon">
      <InputSearch @pesquisar-pokemon="searchPokemon" />

      <PokemonFound
        :pokemonImage="pokemonImage"
        :pokemonName="pokemonName"
        :evolucoes="evolucoes"
        :stats="stats"
        :showInfo="showInfo"
        @pesquisar-pokemon="searchPokemon"
      />
    </section>
  </main>
</template>

<script>
import PokemonFound from "./components/PokemonFound.vue";
import InputSearch from "./components/InputSearch.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      pokemonName: "",
      pokemonImage: "./img/quemeh.png",
      evolucoes: [],
      stats: [],
      showInfo: false,
    };
  },
  components: {
    InputSearch,
    PokemonFound,
  },
  methods: {
    searchPokemon(nome) {
      this.pokemonName = nome;
      this.evolucoes = [];
      this.getPokemon();
    },

    getPokemon() {
      axios
        .get(
          `https://pokeapi.co/api/v2/pokemon/${this.pokemonName.toLocaleLowerCase()}`
        )
        .then((res) => {
          this.pokemonImage = res.data.sprites.front_default;
          this.pokemonName = res.data.species.name;

          console.log("stats", res.data.stats);
          this.stats = res.data.stats;
          this.showInfo = true;

          this.getSpeciesInfo(res.data.species.url);
        })
        .catch((e) => {
          console.log("funcao getPokemon", e);
          this.pokemonImage = "./img/quemeh.png";
          this.stats = [
            {
              base_stat: "--",

              stat: {
                name: "hp",
              },
            },
            {
              base_stat: "--",

              stat: {
                name: "attack",
              },
            },
            {
              base_stat: "--",

              stat: {
                name: "defense",
              },
            },
            {
              base_stat: "--",

              stat: {
                name: "special-attack",
              },
            },
            {
              base_stat: "--",

              stat: {
                name: "special-defense",
              },
            },
            {
              base_stat: "--",

              stat: {
                name: "speed",
              },
            },
          ];
        });
    },

    getSpeciesInfo(url) {
      axios
        .get(url)
        .then((res) => {
          this.getEvolutionsInfo(res.data.evolution_chain.url);
        })
        .catch((err) => console.log("funcao getSpeciesInfo", err));
    },

    getEvolutionsInfo(url) {
      axios
        .get(url)
        .then((res) => {
          console.log(res.data.chain);
          this.evolucoes.push(res.data.chain.species);
          this.percorrerArryDeEvolucoes(res.data.chain.evolves_to);
        })
        .catch((err) => console.log("funcao getEvolutionsInfo", err));
    },

    percorrerArryDeEvolucoes(arr) {
      if (arr.length < 1) {
        console.log("evolucoes", this.evolucoes);
        return undefined;
      }

      this.evolucoes.push(arr[0].species);

      return this.percorrerArryDeEvolucoes(arr[0].evolves_to);
    },
  },
};
</script>

<style></style>
