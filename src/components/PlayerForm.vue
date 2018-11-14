<template>
  <v-card-text>
    <v-subheader class="pa-0">Enter a player name to find their stats.</v-subheader>
    <v-autocomplete
      v-model="playerId"
      :items="players"
      :search-input.sync="search"
      :loading="loading"
      :cache-items="true"
      :persistent-hint="true"
      hint="*try surnames if you don't get desired result"
      placeholder="Dhoni, Kohli, Sharma"
      autofocus
      item-text="Player_Name"
      item-value="Player_Id"
      label="Player Name"
    >
    </v-autocomplete>
  </v-card-text>
</template>

<script>
  import debounce from '../utils/debounce'

  export default {
    data () {
      return {
        playerId: null,
        loading: false,
        players: [],
        search: null
      }
    },
    methods: {
      searchFunc: debounce(async function (val) {
        this.loading = true
        const apiUrl = process.env.VUE_APP_API_URL
        try {
          const res = await fetch(`${apiUrl}/players?q=${val}`).then(res => res.json())
          this.players = res.data
        } catch(error) {
          console.error(error)
        } finally {
          this.loading = false
        }
      }, 300)
    },
    watch: {
      playerId(val) {
        this.$emit('select-player', val)
      },
      search(val) {
        this.searchFunc(val)
      }
    }
  }
</script>
