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

<style scoped>
.pokemon_list-image {
  min-width: 160px;
  max-width: 300px;
  display: flex;
  align-items: center;
}
.pokemon_list-image img {
  width: 80px;
  margin-right: 6px;
}

.pokemon_list-image span {
  font-size: 24px;
  color: #222;
  font-weight: bold;
  transition: 0.5s;
}
.pokemon_list-image span:hover {
  cursor: pointer;
  color: #fff;
}
</style>
