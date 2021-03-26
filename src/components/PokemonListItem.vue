<template>
  <li v-on:click="handleClick">{{ pokemon.name }}</li>
</template>

<script>
import { eventBus } from "@/main.js";

export default {
  name: "pokemon-list-item",
  props: ["pokemon"],
  methods: {
    handleClick() {
      eventBus.$emit("pokemon-selected", this.pokemon);
    },
  },
};
</script>

<style>
</style>