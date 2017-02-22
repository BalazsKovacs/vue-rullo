<template>
  <div class="container">
  <p><button class="btn btn-primary" @click="newGame">New Game</button></p>
  <table>
    <tr>
      <td></td>
      <td v-for="c in cols">
        <sum-cell :current="getCurrentColSum(c)" :expected="getColSum(c)"></sum-cell>
      </td>
      <td></td>
    </tr>

    <tr v-for="(row, i) in board">
      <td>
        <sum-cell :current="getCurrentRowSum(i)" :expected="getRowSum(i)"></sum-cell>
      </td>
      <td v-for="(value, j) in row">
        <cell :item="value" :check="checkFinished"></cell>
      </td>
      <td>
      <sum-cell :current="getCurrentRowSum(i)" :expected="getRowSum(i)"></sum-cell>
      </td>
    </tr>

    <tr>
      <td></td>
      <td v-for="c in cols">
        <sum-cell :current="getCurrentColSum(c)" :expected="getColSum(c)"></sum-cell>
      </td>
      <td></td>
    </tr>
  </table>
</template>

<script>
import Cell from './Cell.vue';
import SumCell from './SumCell.vue';

export default {
  props: ['board', 'onReset'],
  components: {
    cell: Cell,
    sumCell: SumCell
  },
  computed: {
    rows: function() {return this.board.length},
    cols: function() {return this.board[0].length;},
    rowsum: function() {
      return
        this.board.map(row => row.reduce((sum,item) => sum += (item.selected ? item.value : 0),0))
      ;
    }
  },
  methods: {
    getRowSum: function(i) {
      return this.board[i].reduce((sum,item) => sum += (item.isActive ? item.value : 0),0);
    },
    getColSum: function(i) {
      return this.board.map(r => r[(i-1)]).reduce((sum,item) => sum += (item.isActive ? item.value : 0),0);
    },
    getCurrentRowSum: function(i) {
      return this.board[i].reduce((sum,item) => sum += (item.selected ? item.value : 0),0);
    },
    getCurrentColSum: function(i) {
      return this.board.map(r => r[(i-1)]).reduce((sum,item) => sum += (item.selected ? item.value : 0),0);
    },
    newGame: function() {
      this.onReset();
    },
    checkFinished: function() {
      let finished = true;
      for (let i = 0; i < this.rows; i++) {
        if (this.getCurrentRowSum(i) != this.getRowSum(i)) {
            finished = false;
        }
      }

      for (let j = 1; j <= this.cols; j++) {
        if (this.getCurrentColSum(j) != this.getColSum(j)) {
            finished = false;
        }
      }

      if (finished) {
        if (confirm('New game?')) {
          this.onReset();
        }
      }
    }
  }
};
</script>

<style scoped>
  button:not(.btn-primary) {
    width: 45px;
    text-align: center;
    margin: 5px;
    border-radius: 50%;
    border: 1px solid grey;
    line-height: 40px;
  }

  button.locked {
    border: 2px solid black !important;
  }

</style>
