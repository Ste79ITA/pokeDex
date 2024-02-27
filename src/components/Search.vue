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
    <div class="card" style="width: 18rem">
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
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';

const pokeapi = 'https://pokeapi.co/api/v2/pokemon/';
let pokeSearch = ref('');
let pokemonData = ref({});

function search() {
  axios
    .get(pokeapi + pokeSearch.value)
    .then((res) => {
      if (pokeSearch.value.length === 0) {
        return;
      } else {
        console.log(res.data);
        pokemonData.value = {
          image: res.data.sprites.front_default,
          name: res.data.name,
          type: res.data.types[0].type.name,
          height: res.data.height,
          weight: res.data.weight,
          hp: res.data.stats[0].base_stat,
          attack: res.data.stats[1].base_stat,
          defence: res.data.stats[2].base_stat,
          special_attack: res.data.stats[3].base_stat,
          special_defence: res.data.stats[4].base_stat,
          speed: res.data.stats[5].base_stat,
        };
      }
    })
    .catch(function (error) {
      console.log(error.response.data);
    });
}
</script>

<style lang="scss" scoped></style>
