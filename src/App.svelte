<script>
  import Game from './Game.svelte';
</script>

<main>
  <h1>Snake Game</h1>
  <Game />
</main>

<style>
  /* Custom Font */
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
    background: linear-gradient(135deg, #1d1f21, #282c34);
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.3);
  }

  h1 {
    font-family: 'Press Start 2P', cursive;
    font-size: 2.5rem;
    margin-bottom: 20px;
    color: #61dafb;
    text-shadow: 2px 2px 0px #000;
    animation: glow 1.5s infinite alternate;
  }

  /* Glow effect on the title */
  @keyframes glow {
    from {
      text-shadow: 2px 2px 10px #61dafb, 0 0 20px #61dafb, 0 0 30px #61dafb, 0 0 40px #61dafb, 0 0 50px #61dafb, 0 0 60px #61dafb, 0 0 70px #61dafb;
    }
    to {
      text-shadow: 2px 2px 20px #61dafb, 0 0 30px #61dafb, 0 0 40px #61dafb, 0 0 50px #61dafb, 0 0 60px #61dafb, 0 0 70px #61dafb, 0 0 80px #61dafb;
    }
  }

  /* Main container style */
  .grid {
    border: 2px solid #61dafb;
    padding: 5px;
    background-color: #20232a;
    border-radius: 10px;
    box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.3);
  }

  /* Cell style */
  .cell {
    transition: background-color 0.2s ease;
  }

  .snake {
    background-color: #61dafb;
    border-radius: 3px;
  }

  .food {
    background-color: #e91e63;
    border-radius: 50%;
    animation: pulse 1s infinite;
  }

  /* Pulse animation for the food */
  @keyframes pulse {
    0% {
      transform: scale(0.9);
      box-shadow: 0 0 5px #e91e63;
    }
    70% {
      transform: scale(1);
      box-shadow: 0 0 20px #e91e63, 0 0 30px #e91e63;
    }
    100% {
      transform: scale(0.9);
      box-shadow: 0 0 5px #e91e63;
    }
  }
</style>
