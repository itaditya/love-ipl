<template>
  <v-card>
    <v-card-title class="headline font-weight-regular white--text title">Player Batting Performance</v-card-title>
    <PlayerForm v-on:select-player="onSelectPlayer"/>
    <PlayerChart v-if="playerId" :player-id="playerId" :key="playerId"/>
  </v-card>
</template>

<style scoped>
  .title {
    background-color: #575967;
  }
</style>

<script>
import PlayerForm from './PlayerForm'
import PlayerChart from './PlayerChart'

export default {
  components: {
    PlayerForm,
    PlayerChart
  },
  data() {
    return {
      playerId: null
    }
  },
  methods: {
    onSelectPlayer(playerId) {
      this.playerId = playerId
    }
  }
}
</script>
