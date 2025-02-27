<script>
import TicTacToe from './components/TicTacToe.vue';

export default {
  // exporting the component TicTacToe
  components: {
    TicTacToe
  }
};
</script>

<template>
  <div>
    <h1>Tic Tac Toe</h1>
    <TicTacToe />
  </div>
</template>


<style>
#app {
  text-align: center;
  margin-top: 20px;
  font-family: "Comic Sans MS", cursive, sans-serif;
  text-align: center;
}
</style>