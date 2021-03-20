<template>
  <div>
    <div class="text-center bold pb-3">
      Pokemon
    </div>
    <div class="row">
      <div v-for="item in orderedPokemon" :key="item.id" class="col-2 text-center">
        <div>
          <img :src="item.sprites.front_default">
        </div>
        <div>
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// using for sort id of pokemon
import _ from 'lodash'
export default {
  data () {
    return {
      pokemonList: [],
      limit: 104
    }
  },
  async fetch () {
    // first fetch pokemon's data from https://pokeapi.co/api/v2
    await this.$axios.$get('https://pokeapi.co/api/v2'
    ).then((response) => {
      // limit to find pokemon id 1-104
      this.fetchAllPokemonList(response.pokemon + `?limit=${this.limit}`)
    }).catch((error) => {
      alert(error)
    })
  },
  computed: {
    // sort pokemon by id
    orderedPokemon () {
      return _.orderBy(this.pokemonList, 'id')
    }
  },
  methods: {
    // get url from each pokemon (id 1-104)
    async fetchAllPokemonList (url) {
      await this.$axios.$get(url
      ).then((response) => {
        response.results.forEach((pokemon) => {
          this.fetchPokemonData(pokemon)
        })
      }).catch((error) => {
        alert(error)
      })
    },
    // get data of each pokemon
    async fetchPokemonData (pokemon) {
      const url = pokemon.url
      await this.$axios.$get(url
      ).then((response) => {
        this.pokemonList.push(response)
      }).catch((error) => {
        alert(error)
      })
    }
  }
}
</script>
