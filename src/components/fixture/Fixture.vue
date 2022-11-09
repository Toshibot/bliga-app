<template>
  <h2>Spielplan - {{roundNumber}}. Spieltag</h2>
  <span class="fixture-item-container" v-for="fixtureItem in fixtureData" :key="fixtureItem.id">
    <FixtureItem 
      :clubData="clubData"
      :fixtureRoundNumber="fixtureItem.matchday"
      :roundNumber="roundNumber"
      :timestamp="fixtureItem.utcDate"
      :gameStatus="fixtureItem.status"
      :matchStatus="fixtureItem.status"
      :matchTime="fixtureItem.utcDate"
      :teamHome="fixtureItem.homeTeam"
      :teamAway="fixtureItem.awayTeam"
      :score="fixtureItem.score.fullTime"
    />
  </span>
  
</template>
<script lang="ts">
import FixtureItem from "./FixtureItem.vue"

export default {
  components: {
    FixtureItem
  },
  props: {
    fixtureData: {
      type: Object
    },
    clubData: {
      type: Object
    },
    roundName: {
      type: String
    },
    roundNumber: {
      type: Number
    }
  }
}
</script>
<style scoped lang="scss">
  h2 {
    font-size: 24px;
    text-align: center;
    padding-bottom: 12.5px;

    @media screen and (max-width: $break-m) {
      margin-top: 25px;
    }
  }
  .fixture-item-container {
    width: auto;

    @media screen and (max-width: $break-m) {
      display: block;
      width: 100%;
      max-width: 100%;
      padding: 0 12.5px;
    }
  }
</style>
