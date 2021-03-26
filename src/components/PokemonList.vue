<template>
  <ul>
    <pokemon-list-item
      v-for="(pokemon, index) in pokemons"
      :key="index"
      :pokemon="pokemon"
    ></pokemon-list-item>
  </ul>
</template>

<script>
import PokemonListItem from "@/components/PokemonListItem";

export default {
  name: "pokemon-list",
  components: { "pokemon-list-item": PokemonListItem },
  props: ["pokemons"],
};
</script>

<style>
ul {
  height: 100%;
  overflow-y: scroll;
  margin: 0;
}
</style>