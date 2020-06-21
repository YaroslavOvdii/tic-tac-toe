<template>
  <div id="app">
    <Status :player="player" :isGameWon="isGameFinished" :draw="isItADraw" @restart="restartGame()"></Status>
    <div class="cell-group">
      <Cell v-for="(cell, index) in grid" v-bind:key="index"
      :currentPlayer="player" :cellValue="cell" :cellIndex="index" :isGameFinished="isGameFinished"
      :isGameRestarted="restart"
      @changedCellStatus="runCheck($event)"
      @cellRestarted="restart = false"
      ></Cell>
    </div>
  </div>
</template>

<script>
import Cell from './components/Cell.vue';
import Status from './components/Status.vue';

export default {
  name: 'TicTacToe',
  data () {
    return {
      winSquances: [
        [0, 1, 2],
        [0, 4, 8],
        [1, 4, 7],
        [2, 4, 6],
        [3, 4, 5],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [6, 7, 8]

      ],
      grid: ['', '', '', '', '', '', '', '', ''],
      player: 'X',
      isGameFinished: false,
      isItADraw: false,
      restart: false
    }
  },
  components: {
    Cell,
    Status
  },
  methods: {
    runCheck: function(cellIndex) {
      this.grid[cellIndex] = this.player;

      if (this.isPlayerWon()) {
        this.isGameFinished = true;

        return;
      }

      if (this.isItDraw()) {
        this.isGameFinished = true;
        this.isItADraw = true;

        return;
      }

      this.player = this.player === 'X' ? 'O' : 'X';
    },
    isPlayerWon: function() {
      let isPlayerWon = false;

      for (let i = 0; i < this.winSquances.length; i++) {
        let winSquance = this.winSquances[i];
        let cellA = this.grid[winSquance[0]];
        let cellB = this.grid[winSquance[1]];
        let cellC = this.grid[winSquance[2]];

        if (cellA !== '' && cellB !== '' && cellC !== '') {
          if (cellA === cellB && cellB === cellC) {
            isPlayerWon = true;
            debugger;
            break;
          }
        }
      }

      return isPlayerWon;
    },
    isItDraw: function() {
      return !this.grid.includes('');
    },
    restartGame: function() {
      this.grid = ['', '', '', '', '', '', '', '', ''];
      this.restart = true;
      this.player = 'X';
      this.isGameFinished = false;
      this.isItADraw = false;
    }
  }
}
</script>

<style>
  .cell-group {
    display: flex;
    max-width: 600px;
    justify-content: center;
    align-items: center;
    margin: 50px auto;
    flex-wrap: wrap;
  }
</style>
