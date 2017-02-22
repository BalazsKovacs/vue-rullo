<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-sm-12 centered">
        <h1>Rullo</h1>
        <board :board="board" :on-reset="generateBoard"></board>
      </div>
    </div>
  </div>
</template>

<script>
import Board from './components/Board.vue';

export default {
  name: 'app',
  data () {
    return {
      rows: 5,
      cols: 5,
      board: [],
      limit: .35,
      max: 9,
      min: 1
    }
  },
  components: {
    board: Board
  },
  methods: {
    generateBoard: function() {
      let board = [];
      for (let i = 0; i < this.rows; i++) {
        let row = [];
        for (let j = 0; j < this.cols; j++) {
          let cell = {};
          cell.value = parseInt(Math.random() * (this.max - this.min) + this.min);
          cell.selected = true;
          cell.isActive = (Math.random() > this.limit);
          row.push(cell);
        }
        board.push(row);
      }
      this.board = board;
    }
  },
  created: function() {
    this.generateBoard();
  }
}
</script>

<style>
</style>
