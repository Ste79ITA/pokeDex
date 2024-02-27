<template>
  <div class="card" style="width: 18rem">
    <img :src="props.pokemonData.image" alt="" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">Name: {{ props.pokemonData.name }}</h5>
      <h5 class="card-title">Type: {{ props.pokemonData.type }}</h5>
      <h5 class="card-title">Height: {{ props.pokemonData.height }}</h5>
      <h5 class="card-title">Weight: {{ props.pokemonData.weight }}</h5>
      <h5 class="card-title-stats" style="margin-top: 50px">Stats</h5>

      <p class="card-text">Hp {{ props.pokemonData.hp }}</p>
      <p class="card-text">Attack {{ props.pokemonData.attack }}</p>
      <p class="card-text">Defence {{ props.pokemonData.defence }}</p>
      <p class="card-text">
        Special Attack {{ props.pokemonData.special_attack }}
      </p>
      <p class="card-text">
        Special Defence {{ props.pokemonData.special_defence }}
      </p>
      <p class="card-text">Speed {{ props.pokemonData.speed }}</p>

      <a href="#" class="btn btn-primary">Save into PokeDex</a>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['pokemonData']);
</script>

<style lang="scss" scoped></style>
