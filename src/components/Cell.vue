<template>
  <button @click="changeCellStatus()" class="cell" :disabled="isGameFinished || isCellNotEmpty">
    {{ status || cellValue }}
  </button>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    cellIndex: {
      type: Number,
      default: 0
    },
    currentPlayer: {
      type: String,
      default: ''
    },
    cellValue: {
      type: String,
      default: ''
    },
    isGameFinished: {
      type: Boolean,
      default: false
    },
    isGameRestarted: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      status: '',
      isCellNotEmpty: false
    }
  },
  updated: function() {
    if (this.isGameRestarted) {
      this.isCellNotEmpty = false;
      this.status = '';

      this.$emit('cellRestarted');
    }
  },
  methods: {
    changeCellStatus: function() {
      this.status = this.currentPlayer;
      this.isCellNotEmpty = true;

      this.$emit('changedCellStatus', this.cellIndex);
    }
  }
}
</script>

<style>
  .cell {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 1;
    background-color:transparent;
    width: 100%;
    height: 100px;
    border: 1px solid;
    cursor: pointer;
    flex-basis: 33%;
    text-align: center;
    outline: none;
    font-size: 70px;
    color: black;
  }



  .cell:nth-child(1),
  .cell:nth-child(4),
  .cell:nth-child(7) {
    border-left: none;
  }

  .cell:nth-child(1),
  .cell:nth-child(2),
  .cell:nth-child(3) {
    border-top: none;
  }

  .cell:nth-child(3),
  .cell:nth-child(6),
  .cell:nth-child(9) {
    border-right: none;
  }

  .cell:nth-child(7),
  .cell:nth-child(8),
  .cell:nth-child(9) {
    border-bottom: none;
  }

  .cell:hover {
    border-color:green;
    border-width: 3px;
    border-style: solid;
    transition: all 0.1s linear;
  }

  .cell:hover:disabled {
    border-color:red;
  }


</style>
