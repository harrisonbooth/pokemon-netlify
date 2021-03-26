<template>
  <article>
    <h2>{{ pokemon.name }}</h2>
    <img
      :src="pokemon.sprites.front_default"
      :alt="pokemon.name + ` game sprite.`"
    />
  </article>
</template>

<script>
export default {
  name: "pokemon-details",
  props: ["pokemon"],
};
</script>

<style>
h2 {
  margin-top: 0;
}
</style>