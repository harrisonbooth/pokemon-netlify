<template>
  <main>
    <pokemon-list :pokemons="pokemonList"></pokemon-list>
    <pokemon-details
      v-if="selectedPokemon"
      :pokemon="selectedPokemon"
    ></pokemon-details>
  </main>
</template>

<script>
import PokemonList from "@/components/PokemonList";
import PokemonDetails from "@/components/PokemonDetails";
import { eventBus } from "@/main.js";

export default {
  name: "App",
  components: {
    "pokemon-list": PokemonList,
    "pokemon-details": PokemonDetails,
  },
  data() {
    return {
      apiPokemonList: [],
      selectedPokemon: null,
    };
  },
  methods: {
    getPokemonList() {
      fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
        .then((res) => res.json())
        .then((data) => (this.apiPokemonList = data.results));
    },
    getSelectedPokemon(url) {
      fetch(url)
        .then((res) => res.json())
        .then((data) => (this.selectedPokemon = data));
    },
  },
  computed: {
    pokemonList: function () {
      // const capitalisedList = [];

      // for (const pokemon of this.apiPokemonList) {
      //   const capitalisedPokemon = {
      //     ...pokemon,
      //     name: pokemon.name[0].toUpperCase() + pokemon.name.slice(1),
      //   };
      //   capitalisedList.push(capitalisedPokemon);
      // }

      // return capitalisedList;

      return this.apiPokemonList.map((pokemon) => ({
        ...pokemon,
        name: pokemon.name[0].toUpperCase() + pokemon.name.slice(1),
      }));
    },
  },
  mounted() {
    this.getPokemonList();

    eventBus.$on("pokemon-selected", (pokemon) =>
      this.getSelectedPokemon(pokemon.url)
    );
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  height: 100vh;
  padding: 15px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
main {
  display: grid;
  grid-template-columns: 2fr 8fr;
  height: 100%;
  grid-gap: 1em;
}
</style>
