<template>
  <div class="ladder-header">
    <div class="ladder-header-position">
      Pos.
    </div>
    <div class="ladder-header-club">
      Mannschaft
    </div>
    <div class="ladder-header-played">
      Sp
    </div>
    <div class="ladder-header-wins">
      S
    </div>
    <div class="ladder-header-losses">
      U
    </div>
    <div class="ladder-header-draws">
      N
    </div>
    <div class="ladder-header-percentage">
      TD
    </div>
    <div class="ladder-header-points">
      Pkt
    </div>
  </div>
</template>
<style scoped lang="scss">
  .ladder-header {
    display: flex;
    flex: 0 1 auto;
    flex-wrap: wrap;
    margin: 3px auto;
    position: relative;
    text-align: left;
    color: $color-white;
    background: $color-black-dark;

    div {
      display: inline-block;
      height: 41px;
      line-height: 41px;

      &:nth-child(even) {
        background: rgba(0,0,0,0.05);
      }
    }

    &-club {
      flex-basis: 33.333%;
      max-width: 33.333%;
      text-align: left;

      @media screen and (max-width: $break-s) {
        flex-basis: 75%;
        max-width: 75%;
        padding-left: $size-base-s;
      }

      img {
        width: 41px;
        height: 41px;
        margin-bottom: -2px;
        background: $color-grey;
      }

      span {
        padding-left: 12.5px;
        display: inline-block;
        vertical-align: top;
      }
    }

    &-position,
    &-played,
    &-wins,
    &-losses,
    &-draws,
    &-points {
      flex-basis: 8.333%;
      max-width: 8.333%;
      text-align: center;
    }

    &-position {
      @media screen and (max-width: $break-s) {
        display: none !important;
      }
    }

    &-percentage {
      flex-basis: 16.667%;
      max-width: 16.667%;
      text-align: center;

      @media screen and (max-width: $break-s) {
        flex-basis: 8.333%;
        max-width: 8.333%;
      }
    }

    &-wins,
    &-losses,
    &-draws {
      @media screen and (max-width: $break-s) {
        display: none !important;
      }
    }
  }
</style>
<script lang="ts">

export default {
  
}
</script>
