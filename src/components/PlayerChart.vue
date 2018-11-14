<template>
  <v-card-text>
    <template v-if="loading === false">
      <trend
        :data="matchRuns"
        :gradient="['#6fa8dc', '#42b983', '#2c3e50']"
        auto-draw>
      </trend>
      <h4 class="text-xs-center">
        Runs per match
        <span v-if="minScore !== null">
          (Min: {{minScore}} Max: {{maxScore}})
        </span>
      </h4>
    </template>
    <p v-else class="text-xs-center">Crunching some data...</p>
  </v-card-text>
</template>

<script>
export default {
  props: ['playerId'],
  data() {
    return {
      loading: false,
      matchRuns: []
    }
  },
  computed: {
    minScore() {
      if(this.matchRuns.length === 0) {
        return null
      }
      return Math.min(...this.matchRuns)
    },
    maxScore() {
      if(this.matchRuns.length === 0) {
        return null
      }
      return Math.max(...this.matchRuns)
    }
  },
  async mounted() {
    const apiUrl = process.env.VUE_APP_API_URL
    const playerId = this.playerId
    this.loading = true
    try {
      const res = await fetch(`${apiUrl}/playerperf?playerId=${playerId}`).then(res => res.json())
      const perf = res.data;
      this.matchRuns = perf.map(p => p.runs)
    } finally {
      this.loading = false
    }
  }
}
</script>
