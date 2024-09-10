<template>
  <div class="tic-tac-toe">
    <div class="board">
      <div class="cell" v-for="cell in board" :key="cell.index" @click="handleCellClick(cell.index)">
        {{ cell.value }}
      </div>
    </div>
    <p v-if="winner">{{ winner }} wins!</p>
    <p v-else-if="isDraw">It's a draw!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: [
        { index: 0, value: null },
        { index: 1, value: null },
        { index: 2, value: null },
        { index: 3, value: null },
        { index: 4, value: null },
        { index: 5, value: null },
        { index: 6, value: null },
        { index: 7, value: null },
        { index: 8, value: null },
      ],
      currentPlayer: 'X',
      winner: null,
      isDraw: false,
    };
  },
  methods:   {
    handleCellClick(index) {
      if (this.board[index].value || this.winner) return;
      this.board[index].value = this.currentPlayer;
      this.checkWinner();
      this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (const combination of winningCombinations) {
        if (
          this.board[combination[0]].value !== null &&
          this.board[combination[0]].value === this.board[combination[1]].value &&
          this.board[combination[1]].value === this.board[combination[2]].value
        ) {
          this.winner = this.board[combination[0]].value;
          return;
        }
      }

      if (!this.board.some((cell) => cell.value === null)) {
        this.isDraw = true;
      }
    },
  },
};
</script>

<style>
.tic-tac-toe {
  display: flex;
  justify-content: center;
  align-items: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}

.cell {
  width: 80px;
  height: 80px;
  border: 1px solid #ccc;
  text-align: center;
  font-size: 30px;
  cursor: pointer;
}
</style>

