## Hi there 👋

<!--
**fernando-cotrena/fernando-cotrena** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Snake Game</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #111;
      margin: 0;
    }
    canvas {
      background: #000;
      border: 2px solid #0f0;
    }
  </style>
</head>
<body>
  <canvas id="game" width="400" height="400"></canvas>
  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");

    const box = 20;
    let snake = [{ x: 9 * box, y: 9 * box }];
    let direction;
    let food = {
      x: Math.floor(Math.random() * 20) * box,
      y: Math.floor(Math.random() * 20) * box
    };

    document.addEventListener("keydown", e => {
      if (e.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
      if (e.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
      if (e.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
      if (e.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
    });

    function draw() {
      ctx.clearRect(0, 0, 400, 400);

      // dibujar comida
      ctx.fillStyle = "red";
      ctx.fillRect(food.x, food.y, box, box);

      // dibujar serpiente
      for (let i = 0; i < snake.length; i++) {
        ctx.fillStyle = i === 0 ? "lime" : "green";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
      }

      // posición cabeza
      let snakeX = snake[0].x;
      let snakeY = snake[0].y;

      if (direction === "LEFT") snakeX -= box;
      if (direction === "UP") snakeY -= box;
      if (direction === "RIGHT") snakeX += box;
      if (direction === "DOWN") snakeY += box;

      // comer
      if (snakeX === food.x && snakeY === food.y) {
        food = {
          x: Math.floor(Math.random() * 20) * box,
          y: Math.floor(Math.random() * 20) * box
        };
      } else {
        snake.pop();
      }

      const newHead = { x: snakeX, y: snakeY };

      // colisiones
      if (
        snakeX < 0 || snakeY < 0 || snakeX >= 400 || snakeY >= 400 ||
        snake.some(part => part.x === newHead.x && part.y === newHead.y)
      ) {
        clearInterval(game);
        alert("Game Over");
      }

      snake.unshift(newHead);
    }

    const game = setInterval(draw, 100);
  </script>
</body>
</html>
