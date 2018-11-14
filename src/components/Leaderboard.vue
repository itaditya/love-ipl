<template>
  <div>
    <v-card>
      <v-card-title class="headline font-weight-regular blue-grey white--text">Leaderboard</v-card-title>
      <v-list>
        <v-list-tile v-for="team in teams" :key="team._id">
          <v-list-tile-content>
            <v-list-tile-title>{{team.name}}</v-list-tile-title>
          </v-list-tile-content>
          <v-list-tile-action class="text-xs-right text-md-right text-lg-right">
            <v-list-tile-sub-title>{{team.wins}} wins</v-list-tile-sub-title>
          </v-list-tile-action>
        </v-list-tile>
      </v-list>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      teams: []
    }
  },
  mounted() {
    const apiUrl = process.env.VUE_APP_API_URL
    fetch(`${apiUrl}/leaderboard`)
    .then(res => res.json())
    .then(res => {
      const teamsInfo = res.data
      this.teams = teamsInfo.map(item => {
        const team = item.team[0]
        return {
          name: team.Team_Name,
          wins: item.wonMatches
        }
      })
    })
  }
}
</script>
