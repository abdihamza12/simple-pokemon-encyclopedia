<script>
import { ref } from "vue";
export default {
  setup() {
    let pokeData = ref([]);
    function getPokeInfo(pokemon) {
      fetch("https://pokeapi.co/api/v2/pokemon/" + pokemon)
        .then((data) => {
          return data.json();
        })
        .then((post) => {
          this.pokeData = post;
          // console.log(pokeData);
          // console.log(pokeData);
        });
    }
    return {
      pokeData,
      getPokeInfo,
    };
  },
};
</script>

<template>
  <div>
    <form @submit.prevent="getPokeInfo(pokemonName)">
      <button type="submit">Get Pokemon Data</button> <br />
      <input name="pokemonName" v-model="pokemonName" type="text" />
    </form>

    <!-- <button @click="getPokeInfo('charizard')">Get Charizard Info</button><br /> -->
    <img :src="pokeData.sprites?.front_default" alt="" />
    <h2>Type:</h2>
    <ul>
      <li :key="index" v-for="(type, index) in pokeData.types">
        {{ type.type.name }}
      </li>
    </ul>
    <h2>Base Stats:</h2>
    <ul>
      <li :key="index" v-for="(stat, index) in pokeData.stats">
        {{ stat.stat.name }}: {{ stat.base_stat }}
      </li>
    </ul>
    <h2>Abilities:</h2>
    <ul>
      <li :key="index" v-for="(ability, index) in pokeData.abilities">
        {{ ability.ability.name }}
      </li>
    </ul>
    <h2>Weight:</h2>
    <p>{{ pokeData.weight }}</p>
    <h2></h2>
    <h2></h2>
  </div>
</template>

<style></style>
