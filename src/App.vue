<script setup lang="ts">
  // Vue Components
  import IconKit from "./components/icons/IconKit.vue";
  import Fixture from "./components/fixture/Fixture.vue";
  import Ladder from "./components/ladder/Ladder.vue";
</script>

<template>
  <body id="Body" class="t-dark">
    <main class="o-main u-vert-center">
      <section class="o-section u-flex">
        <h1 class="o-section__title">Saison 22/23</h1>
        <article class="c-ladder__container u-col-5@lg u-col-12@md u-padding-col">
          <div class="js-ladder">
              <Ladder :ladderData="ladderData" :clubData="clubData" />
          </div>
        </article>
        <article class="u-col-7@lg u-col-12@md u-padding-col@md">
          <div class="c-fixture">
            <div class="js-fixture">
              <Fixture :fixtureData="fixtureData" :clubData="clubData" :roundNumber="roundNumber" />
            </div>
          </div>
        </article>
      </section>
    </main>
  </body>
</template>

<style scoped lang="scss">

</style>
<script lang="ts">
import axios from 'axios';

export default {
  components: {
    IconKit,
    Fixture,
    Ladder
  },
  data() {
    return {
      ladderData: [],
      roundNumber: 0,
      fixtureData: [],
      clubData: []
    }
  },
  mounted() {
    // Club Data - Hosted
    axios.get('./data/data-teams.json')
      .then(response => {
        console.log(response.data)
        this.clubData = response.data;
      })
    // Ladder Data - Remote
    axios.get('https://api.football-data.org/v2/competitions/2002/standings', {
      headers:{
        "X-Auth-Token": "5c8b70988e784fca8186b93d38b1bae7"
      }
    })
      .then(response => {
        console.log(response.data)
        console.log(response.data.season.currentMatchday)
        this.ladderData = response.data.standings[0].table;
        this.roundNumber = response.data.season.currentMatchday;
      })
      .catch(function (error) {
        console.log(error)
      })
    // Fixture Data - Remote
    axios.get('https://api.football-data.org/v2/competitions/2002/matches', {
      headers:{
        "X-Auth-Token": "5c8b70988e784fca8186b93d38b1bae7"
      }
    })
      .then(response => {
        console.log(response.data);
        this.fixtureData = response.data.matches;
      })
      .catch(function (error) {
        console.log(error)
      })
  },
  methods: {
    getFinals(fixtureData:any){
      for (let i = 0; i < fixtureData.length; i++) {
        if (fixtureData[i].is_final === true) {
          return fixtureData[i];
        }
      }
    }
  }
}
</script>
<style scoped lang="scss">
  .t-dark {
    color: $color-white;
    background-color: $color-black;
  }
  .hidden {
    display: none;
  }
  .o-section__title {
    width: 100%;
    text-align: center;
    font-size: 24px;
    padding: 12.5px 0;
    margin-bottom: 12.5px;
    background: $color-black-dark;
  }
  .c-ladder__container {
    @include flex-size($width-5);

    @media screen and (max-width: $break-m) {
      @include flex-size($width-12)
    }
  }
  .c-fixture {
    text-align: center;
  }
</style>

