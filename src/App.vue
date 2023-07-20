<template>
  <main>
      <div>
        <img :src="imagePokemon" alt="pokemon" class="pokemon-image" />
      </div>

      <h1 class="pokemon-data">
        <span class="pokemon-number"> {{ pokemon ? pokemon.id : 'Loading...' }} - </span>
        <span class="pokemon-name">{{ pokemon ? pokemon.name : '' }}</span>
      </h1>

      <div>
        <form class="form">
          <input
            class="input-search"
            placeholder="Name or Number"
            v-model="params"
            @change="getPokemon(params)"
            required
          />
        </form>

        <div class="buttons">
          <button class="button btn-prev">Prev &lt;</button>
          <button class="button btn-next">Next &gt;</button>
        </div>
      </div>

      <img src="./assets/pokedex.png" alt="pokedex" class="pokedex" />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import axios from 'axios'

export default defineComponent({
  data() {
    return {
      pokemon: {},
      teste: 'variavel',
      params: 1,
      imagePokemon: ''
    }
  },
  created() {
    this.getPokemon(this.params)
  },
  methods: {
    async getPokemon(params) {
      await axios
        .get(`https://pokeapi.co/api/v2/pokemon/${params}`)
        .then(response => {
          const { data } = response;
          this.pokemon = data;
          this.imagePokemon = data["sprites"]["versions"]["generation-v"]["black-white"]["animated"][    "front_default"];
        })
        .catch(error => console.warn(error))
    }
  }
})
</script>