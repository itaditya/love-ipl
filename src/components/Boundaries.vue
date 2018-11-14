<template>
  <div>
    <v-card class="boundary-card elevation-6 six-card">
      <div class="boundary-title">
        <span class="boundary-stat">{{sixes}}</span>
        <span class="boundary-type">sixes</span>
      </div>
    </v-card>
    <v-card class="boundary-card elevation-6 four-card">
      <div class="boundary-title">
        <span class="boundary-stat">{{fours}}</span>
        <span class="boundary-type">fours</span>
      </div>
    </v-card>
    <p class="text-lg-right">*for all seasons so far</p>
  </div>
</template>

<style scoped>
  .boundary-card {
    padding: 10px;
    background-size: cover;
    background-color: rgba(0,0,0,0.4);
    background-blend-mode: overlay;
    background-position-x: 35%;
  }

  .six-card {
    background-image: url('/six-bg.jpg');
    margin-bottom: 40px;
  }

  .four-card {
    background-image: url('/four-bg.jpg');
    margin-bottom: 20px;
  }

  .boundary-title {
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    margin-top: 100px;
    color: #fff;
  }

  .boundary-stat {
    font-size: 54px;
    line-height: 55px;
    padding-right: 8px;
  }

  .boundary-type {
    font-size: 24px;
  }
</style>

<script>
export default {
  data() {
    return {
      sixes: 0,
      fours: 0
    }
  },
  methods: {
    animateSix(six) {
      const sixMax = parseInt(six / 60) * 60
      const sixRem = six % 60

      const repeatOften = () => {
        if(this.sixes < sixMax) {
          this.sixes += 60
          requestAnimationFrame(repeatOften);
        } else {
          this.sixes += sixRem
        }
      }
      requestAnimationFrame(repeatOften);
    },
    animateFour(four) {
      const fourMax = parseInt(four / 110) * 110
      const fourRem = four % 110

      const repeatOften = () => {
        if(this.fours < fourMax) {
          this.fours += 110
          requestAnimationFrame(repeatOften);
        } else {
          this.fours += fourRem
        }
      }
      requestAnimationFrame(repeatOften);
    }
  },
  async mounted() {
    const apiUrl = process.env.VUE_APP_API_URL
    const res = await fetch(`${apiUrl}/boundaries`).then(res => res.json())
    const { six, four } = res.data
    this.animateSix(six)
    this.animateFour(four)
  }
}
</script>
