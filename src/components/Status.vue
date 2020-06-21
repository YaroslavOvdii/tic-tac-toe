<template>
  <div class="status-holder">
    <h2 v-if="!isGameWon">Player <span>{{ player }}</span> turn</h2>
    <h2 v-else-if="isGameWon && draw">No one have win it is a DRAW! <a href="#" @click.prevent="$emit('restart')">Restart Game</a></h2>
    <h2 v-else>The <span>{{ player }}</span> player has won! <a href="#" @click.prevent="$emit('restart')">Restart Game</a></h2>
  </div>
</template>

<script>
export default {
  props: {
    isGameWon: {
      type: Boolean,
      default: false
    },
    player: {
      type: String,
      default: 'X'
    },
    draw: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style>
  .status-holder h2{
    text-align: center;
  }

  .status-holder span {
    font-size: 1.2em;
    color: green;
  }
</style>
