<template>
  <v-app>
    <v-navigation-drawer
      app
      fixed
      clipped
      floating
      mobile-break-point='800'
      class="sidebar"
    >
      <Boundaries />
    </v-navigation-drawer>
    <v-toolbar
      app
      color="#2d2f38"
      dark
      class="navbar"
    >
      <v-toolbar-title>Love IPL</v-toolbar-title>
    </v-toolbar>
    <v-navigation-drawer
      app
      fixed
      clipped
      floating
      right
      mobile-break-point='800'
      width='320'
      class="sidebar"
    >
      <Leaderboard/>
    </v-navigation-drawer>
    <v-content>
      <div class="content">
        <section class="player-section">
          <PlayerStats/>
        </section>
        <section>
          <DreamTeam/>
        </section>
      </div>
    </v-content>
  </v-app>
</template>

<style scoped>
  .navbar {
    padding-left: 0 !important;
  }

  .sidebar {
    background-color: transparent;
    padding: 40px 10px 0;
  }

  .player-section {
    margin-top: 40px;
    margin-bottom: 40px;
  }
  
  .content {
    padding: 0 20px 50px;
  }
</style>

<script>
import Boundaries from './components/Boundaries'
import Leaderboard from './components/Leaderboard'
import DreamTeam from './components/DreamTeam'
import PlayerStats from './components/PlayerStats'

export default {
  name: 'App',
  components: {
    Boundaries,
    Leaderboard,
    DreamTeam,
    PlayerStats
  }
}
</script>
