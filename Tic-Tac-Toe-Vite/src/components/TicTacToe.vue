<!-- Creating TicTacToe template -->
<template>
    <div class="container">
        <hr />
        <button @click="startGame">Reset The Game!</button>
        <div class="board">
            <!-- using v-for directive to create the cells of the board -->
            <!-- using v-bind directive to bind the winner class dynamically to highlight the winningCells  -->
            <div v-for="(cell, index) in board" :key="index" class="cell"
                :class="{ winner: winningCells.includes(index) }" @click="play(index)">
                {{ cell }}
            </div>
        </div>
        <h2 v-if="winner" :class = "{winmessage: true}">{{ winner }} Wins!</h2>
        <h2 v-else-if="isDraw && !winner" :class = "{drawmessage: true}">It's a Draw!</h2>
        <h2 v-else> {{ currentPlayer }}'s Turn! </h2>
    </div>
</template>

<script>
export default {
    data() {
        return {
            board: ["", "", "", "", "", "", "", "", ""],
            currentPlayer: "X",
            winner: null,
            winningCells: [],
            isDraw: false,
        };
    },
    methods: {
        play(index) {
            if (!this.board[index] && !this.winner) {
                this.board[index] = this.currentPlayer;  // update the current move
                if (this.checkWinner()) {
                    this.winner = this.currentPlayer;
                }
                else if (this.board.every(cell => cell !== "")) {
                    this.isDraw = true;
                }
                else {
                    this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
                }
            }
        },
        checkWinner() {
            const winningCombinations = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
                [0, 4, 8], [2, 4, 6]  // Diagonals
            ];

            for (const combination of winningCombinations) {
                const [a, b, c] = combination;
                if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
                    this.winner = this.board[a];
                    this.winningCells = combination;
                    return;
                }
            }
        },
        startGame() {
            this.board = ["", "", "", "", "", "", "", "", ""];
            this.currentPlayer = "X";
            this.winner = null;
            this.winningCells = [];
            this.isDraw = false;
        }
    }
};
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 50vh;
    gap: 20px;
    padding: 30px;
}

.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 5px;
    top: 10px;
}

.cell {
    width: 100px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid black;
    font-size: 2em;
    cursor: pointer;
}

.winner {
    background-color: yellow;
}
.winmessage{
    color: green;
}
.drawmessage{
    color: red;
}
button {
    margin-top: 10px;
    padding: 10px;
    font-size: 16px;
}

h2 {
    width: max-content;
    font-weight: 500;
}
</style>