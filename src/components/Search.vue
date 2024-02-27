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

    <div class="card" style="width: 18rem" v-if="searchSuccess == true">
      <img :src="pokemonData.image" alt="" class="card-img-top" />
      <div class="card-body">
        <h5 class="card-title">Name: {{ pokemonData.name }}</h5>
        <h5 class="card-title">Type: {{ pokemonData.type }}</h5>
        <h5 class="card-title">Height: {{ pokemonData.height }}</h5>
        <h5 class="card-title">Weight: {{ pokemonData.weight }}</h5>
        <h5 class="card-title">Stats</h5>

        <p class="card-text">hp {{ pokemonData.hp }}</p>
        <p class="card-text">attack {{ pokemonData.attack }}</p>
        <p class="card-text">defence {{ pokemonData.defence }}</p>
        <p class="card-text">special attack {{ pokemonData.special_attack }}</p>
        <p class="card-text">
          special defence {{ pokemonData.special_defence }}
        </p>
        <p class="card-text">speed {{ pokemonData.speed }}</p>

        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
    <div class="card" style="width: 18rem" v-if="searchError == true">
      <div class="card-body">
        <h5 class="card-title">Nessun Pokemon trovato</h5>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref, computed } from 'vue';

const pokeapi = 'https://pokeapi.co/api/v2/pokemon/';
let pokeSearch = ref('');
let searchSuccess = ref(false);
let searchError = ref(false);
let axiosData = ref({});
let pokemonData = computed(() => {
  return {
    image: axiosData.sprites.front_default,
    name: axiosData.name,
    type: axiosData.types[0].type.name,
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
