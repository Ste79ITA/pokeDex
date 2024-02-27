<template>
  <div class="container d-flex">
    <form action="GET" @submit.prevent="search()">
      <input
        type="input"
        id="input"
        placeholder="Search your Pokemon"
        v-model="pokeSearch"
      />
      <button type="submit">Search</button>
    </form>
    <template v-if="searchSuccess == true">
      <PokemonCard :pokemonData="pokemonData" />
    </template>
    <div class="card" style="width: 18rem" v-else-if="searchError == true">
      <div class="card-body">
        <h5 class="card-title">Nessun Pokemon trovato</h5>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref, computed } from 'vue';
import PokemonCard from './PokemonCard.vue';

const pokeapi = 'https://pokeapi.co/api/v2/pokemon/';
let pokeSearch = ref('');
let searchSuccess = ref(false);
let searchError = ref(false);
let axiosData = ref({});
let pokemonData = computed(() => {
  const capitalizeFirstLetter = (string) => {
    return string.charAt(0).toUpperCase() + string.slice(1);
  };

  return {
    image: axiosData.sprites.front_default,
    name: capitalizeFirstLetter(axiosData.name),
    type: capitalizeFirstLetter(axiosData.types[0].type.name),
    height: axiosData.height,
    weight: axiosData.weight,
    hp: axiosData.stats[0].base_stat,
    attack: axiosData.stats[1].base_stat,
    defence: axiosData.stats[2].base_stat,
    special_attack: axiosData.stats[3].base_stat,
    special_defence: axiosData.stats[4].base_stat,
    speed: axiosData.stats[5].base_stat,
  };
});

function search() {
  axios
    .get(pokeapi + pokeSearch.value)
    .then((res) => {
      if (pokeSearch.value.length === 0) {
        return;
      } else {
        axiosData = res.data;
        searchError.value = false;
        searchSuccess.value = true;
      }
    })
    .catch(function (error) {
      console.log(error.response.data);
      searchSuccess.value = false;
      searchError.value = true;
    });
}
</script>

<style lang="scss" scoped></style>
