<script>
  import Game from './Game.svelte';
</script>

<main>
  <h1>Snake Game</h1>
  <Game />
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
  }

  h1 {
    font-size: 2rem;
    margin-bottom: 20px;
  }
</style>
