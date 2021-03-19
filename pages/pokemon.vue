<template>
  <div>
    <div>
      Pokemon
    </div>
    <div class="row">
      <div v-for="item in pokemonList" :key="item.id" class="col-2 text-center">
        <div>
          {{ item.id }}
          <img :src="item.sprites.front_default">
          <!-- {{ item.sprites }} -->
        </div>
        <div>
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      pokemonList: [],
      limit: 104
    }
  },
  async fetch () {
    await this.$axios.$get('https://pokeapi.co/api/v2'
    ).then((response) => {
      // console.log(response)
      this.manageUrl(response.pokemon)
    }).catch((error) => {
      console.log(error)
    })
  },
  computed: {
  },
  methods: {
    async manageUrl (url) {
      await this.$axios.$get(url
      ).then((response) => {
        let manageUrl = this.removeParam('offset', response.next)
        manageUrl = this.removeParam('limit', manageUrl)
        this.fetchAllPokemonList(manageUrl + `?limit=${this.limit}`)
      }).catch((error) => {
        console.log(error)
      })
    },
    async fetchAllPokemonList (url) {
      await this.$axios.$get(url
      ).then((response) => {
        response.results.forEach((pokemon) => {
          this.fetchPokemonData(pokemon)
        })
      }).catch((error) => {
        console.log(error)
      })
    },
    async fetchPokemonData (pokemon) {
      const url = pokemon.url
      await this.$axios.$get(url
      ).then((response) => {
        // console.log(response)
        this.pokemonList.push(response)
      }).catch((error) => {
        console.log(error)
      })
    },
    removeParam (key, sourceURL) {
      let rtn = sourceURL.split('?')[0]
      let param
      let paramsArr = []
      const queryString = (sourceURL.includes('?')) ? sourceURL.split('?')[1] : ''
      if (queryString !== '') {
        paramsArr = queryString.split('&')
        for (let i = paramsArr.length - 1; i >= 0; i -= 1) {
          param = paramsArr[i].split('=')[0]
          if (param === key) {
            paramsArr.splice(i, 1)
          }
        }
        if (paramsArr.length) { rtn = rtn + '?' + paramsArr.join('&') }
      }
      return rtn
    }

  }
}
</script>
