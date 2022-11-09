<template>
  <h2>Tabelle</h2>
  <LadderHeader />
  <div v-for="ladderitem in ladderData" :key="ladderitem.id">
    <LadderItem 
      :position="ladderitem.position"
      :clubicon="clubData[ladderitem.team.id].logo"
      :clubname="clubData[ladderitem.team.id].name"
      :played="ladderitem.playedGames"
      :wins="ladderitem.won"
      :losses="ladderitem.lost"
      :draws="ladderitem.draw"
      :goaldifference="ladderitem.goalDifference"
      :points="ladderitem.points"
    />
  </div>
</template>
<script lang="ts">
import LadderHeader from './LadderHeader.vue';
import LadderItem from './LadderItem.vue';

export default {
  components: {
    LadderHeader,
    LadderItem
  },
  props: {
    ladderData: {
      type: Object
    },
    clubData: {
      type: Object
    }
  }
}
</script>
<style scoped lang="scss">
  h2 {
    text-align: center;
    font-size: 24px;
    padding-bottom: 9.5px;
  }
</style>
