<template>
  <div class="fixture-item" :class="[{current: fixtureRoundNumber === roundNumber, live: gameStatus === 'LIVE', post: gameStatus === 'FINISHED'}]">
    <div class="fixture-date">
      <span v-if="gameStatus === 'SCHEDULED' || gameStatus === 'FINISHED'">
        <span class="fixture-date-day">{{gameTime(timestamp).day}}</span>
        <span class="fixture-date-month">{{gameTime(timestamp).month}}</span>
        <span class="fixture-date-date">{{gameTime(timestamp).date}}</span>
      </span>
      <span v-if="gameStatus === 'SCHEDULED'" class="fixture-date-time">{{gameTime(timestamp).time}}</span>
      <span v-else-if="gameStatus === 'FINISHED'" class="fixture-date-time">FT</span>
      <span v-else-if="gameStatus === 'LIVE'" class="fixture-date-time">
        <span class="fixture-live">LIVE </span>
        {{matchStatus}} {{matchTime}}
      </span>
    </div>
    <FixtureTeam 
      :kitsource="homeTeamKit(clubData, teamHome.id)"
      :gameStatus="gameStatus"
      :teamname="clubData[teamHome.id].name"
      :totalscore="score.homeTeam"
    />
    <div class="fixture-vs">vs</div>
    <FixtureTeam 
      :kitsource="awayTeamKit(clubData, teamHome.id, teamAway.id)"
      :gameStatus="gameStatus"
      :teamname="clubData[teamAway.id].name"
      :totalscore="score.awayTeam"
    />
  </div>
</template>
<script lang="ts">
import FixtureTeam from './FixtureTeam.vue'

export default {
    props: {
      clubData: {
        type: Object
      },
      gameStatus: {
        type: String
      },
      matchStatus: {
        type: String
      },
      matchTime: {
        type: String
      },
      fixtureRoundNumber: {
        type: Number
      },
      roundNumber: {
        type: Number
      },
      timestamp: {
        type: String
      },
      date: {
        type: String,
        required: false
      },
      day: {
        type: String,
        required: false
      },
      month: {
        type: String,
        required: false
      },
      time: {
        type: String,
        required: false
      },
      venue: {
        type: String,
        required: false
      },
      teamHome: {
        type: Object
      },
      teamAway: {
        type: Object
      },
      score: {
        type: Object
      }
    },
    components: { FixtureTeam },
    methods: {
      homeTeamKit(clubData:any, teamkey: any) {
        return clubData[teamkey].kits.home.file
      },
      awayTeamKit(clubData:any, hometeamkey: any, awayteamkey: any) {
        return clubData[awayteamkey].kits.away.file
      },
      gameTime(timestamp:any) {
        let date = new Date(timestamp);
        let dayValue = date.getDay();
        let monthValue = date.getMonth();
        let dateValue = date.getDate();
        let hoursValue = date.getHours();
        let minutesValue = date.getMinutes();
        let daysOfTheWeek = [
          "Sunday", 
          "Monday", 
          "Tuesday", 
          "Wednesday", 
          "Thursday", 
          "Friday", 
          "Saturday"
        ];
        let monthsOfTheYear = [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December"
        ];
        return {
          day: daysOfTheWeek[dayValue],
          month: monthsOfTheYear[monthValue],
          date: dateValue,
          time: hoursValue + ':' + minutesValue
        }
      }
    }
}
</script>
<style scoped lang="scss">
  .fixture-item {
    display: none;
    @include borderBox();
    background: $color-grey-dark;
    color: $color-white;
    text-align: center;

    &.live {
      background: $color-white;
      color: $color-black;
    }

    &.post {
      background: #444;
    }
    &.current {
      display: inline-block;
      margin: 0 17px 17px 0;
      padding: 23px 17px 44.5px;
      width: 350px;

      @media screen and (max-width: $break-m) {
        width: 100%;
        margin: 0 0 17px;
      }
    }
  }

  .fixture-date {
    padding: 26px 0 3px;
    line-height: 1.5;
    font-weight: 600;

    &-day,
    &-month,
    &-date {
      margin-right: 5px; 
    }

    &-time {
      font-weight: 400;
    }
  }

  .fixture-live {
    color: $color-red;
    font-weight: 600;
  }

  .fixture-vs {
    display: inline-block;
    padding: 0 25px;
    vertical-align: top;
    margin-top: 50px;
  }

  .fixture-venue {
    padding: 25px 0 30px;
    font-size: 12px;
  }
</style>
