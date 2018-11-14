<template>
  <v-card>
    <v-card-title class="headline font-weight-regular white--text title">Dream Team of the Season</v-card-title>
    <v-card-text>
      <v-data-table
          :headers="headers"
          :items="players"
          :loading="loading"
          :disable-initial-sort="true"
          :hide-actions="true"
        >
          <template slot="items" slot-scope="props">
            <td>
              <span>
                {{ props.item.name }}
              </span>
              <v-chip small v-if="props.item.captain === true">Captain</v-chip>
            </td>
            <td>{{ props.item.country }}</td>
            <td>{{ props.item.stat }}</td>
            <td>
              <img
                v-if="props.item.role === 'Batting'"
                src="/bat.svg"
                class="bat-icon"
              />
              <img
                v-else-if="props.item.role === 'Balling'"
                src="/ball.svg"
                class="ball-icon"
              />
              <img
                v-else
                src="/keep.svg"
                class="keep-icon"
              />
              <span>
                {{ props.item.role }}
              </span>
            </td>
          </template>
        </v-data-table>
      </v-card-text>
    </v-card>
</template>

<style scoped>
  .title {
    background-color: #282a36;
  }

  .bat-icon {
    width: 20px;
  }

  .ball-icon {
    width: 18px;
    padding-right: 5px;
  }

  .keep-icon {
    width: 20px;
    padding-right: 5px;
  }
</style>

<script>
  export default {
    data() {
      return {
        loading: false,
        headers: [
          {
            text: 'Player Name',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          {
            text: 'Country',
            align: 'left',
            value: 'country'
          },
          {
            text: 'Stat',
            align: 'left',
            sortable: false,
            value: 'stat'
          },
          {
            text: 'Role',
            align: 'left',
            value: 'role'
          }
        ],
        players: []
      }
    },
    mounted() {
      const apiUrl = process.env.VUE_APP_API_URL
      this.loading = true
      fetch(`${apiUrl}/dreamteam`)
      .then(res => res.json())
      .then(res => {
        const { batsmen, ballers } = res.data
        const batsmenList = batsmen.map(batsman => {
          const player = batsman.player[0]
          return {
            name: player.Player_Name,
            country: player.Country,
            stat: `${batsman.totalRuns} runs`,
            role: 'Batting'
          }
        })

        const ballersList = ballers.map(baller => {
          const player = baller.player[0]
          return {
            name: player.Player_Name,
            country: player.Country,
            stat: `${baller.wickets} wickets`,
            role: 'Balling'
          }
        })

        const wicketKeeper = {
          name: 'Ms Dhoni',
          country: 'India',
          captain: true,
          stat: '57 Stumpings',
          role: 'Wicket Keeping'
        }

        this.players = [...batsmenList, wicketKeeper, ...ballersList]
      }).finally(() => {
        this.loading = false
      })
    }
  }
</script>
