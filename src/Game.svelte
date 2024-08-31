<script>
  import { onMount } from 'svelte';

  const gridSize = 20;
  const initialSnake = [{ x: 10, y: 10 }];
  const initialDirection = { x: 0, y: 0 };
  const initialFood = { x: Math.floor(Math.random() * gridSize), y: Math.floor(Math.random() * gridSize) };

  let snake = [...initialSnake];
  let direction = { ...initialDirection };
  let food = { ...initialFood };
  let gameInterval;

  const startGame = () => {
    direction = { x: 1, y: 0 };
    snake = [...initialSnake];
    food = { ...initialFood };

    gameInterval = setInterval(() => {
      const newHead = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };

      // Check for wall collision
      if (newHead.x < 0 || newHead.x >= gridSize || newHead.y < 0 || newHead.y >= gridSize) {
        clearInterval(gameInterval);
        alert('Game Over! You hit a wall.');
        return;
      }

      // Check for self collision
      if (snake.some(segment => segment.x === newHead.x && segment.y === newHead.y)) {
        clearInterval(gameInterval);
        alert('Game Over! You ran into yourself.');
        return;
      }

      snake = [newHead, ...snake];

      // Check for food collision
      if (newHead.x === food.x && newHead.y === food.y) {
        food = { x: Math.floor(Math.random() * gridSize), y: Math.floor(Math.random() * gridSize) };
      } else {
        snake.pop();
      }
    }, 200);
  };

  const changeDirection = (event) => {
    const { key } = event;
    if (key === 'ArrowUp' && direction.y === 0) direction = { x: 0, y: -1 };
    if (key === 'ArrowDown' && direction.y === 0) direction = { x: 0, y: 1 };
    if (key === 'ArrowLeft' && direction.x === 0) direction = { x: -1, y: 0 };
    if (key === 'ArrowRight' && direction.x === 0) direction = { x: 1, y: 0 };
  };

  onMount(() => {
    window.addEventListener('keydown', changeDirection);
    startGame();

    return () => {
      window.removeEventListener('keydown', changeDirection);
      clearInterval(gameInterval);
    };
  });
</script>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(20, 20px);
    grid-template-rows: repeat(20, 20px);
    gap: 1px;
  }
  .cell {
    width: 20px;
    height: 20px;
    background-color: #ddd;
  }
  .snake {
    background-color: #333;
  }
  .food {
    background-color: red;
  }
</style>

<div class="grid">
  {#each Array(gridSize * gridSize) as _, index}
    <div class="cell {getCellClass(index)}"></div>
  {/each}
</div>

<script>
  function getCellClass(index) {
    const x = index % gridSize;
    const y = Math.floor(index / gridSize);
    const isSnake = snake.some(segment => segment.x === x && segment.y === y);
    const isFood = food.x === x && food.y === y;
    return isSnake ? 'snake' : isFood ? 'food' : '';
  }
</script>
