<template>
  <li>
    <div class="pokemon_list-image">
      <img :src="image" alt="imagem do pokemon" />
      <span>{{ pokemon.name }}</span>
    </div>
  </li>
</template>

<script>
import axios from "axios";

export default {
  name: "Evolutions",
  props: {
    pokemon: Object,
  },

  data() {
    return {
      image: "../../public/img/quemeh.png",
    };
  },

  mounted() {
    axios
      .get(
        `https://pokeapi.co/api/v2/pokemon/${this.pokemon.name.toLocaleLowerCase()}`
      )
      .then((res) => {
        this.image = res.data.sprites.front_default;
      })
      .catch((e) => console.log("funcao getPokemon", e));
  },
};
</script>

<style scoped></style>
