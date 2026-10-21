# Eu me chamo Yasmim 👋
- Olá, seja bem-vindo(a)! 
- Sou apaixonada por tecnologia e estou sempre em busca de aprender algo novo.  
- Python, C#, CSS, JavaScript, SQL, HTML.

# Sobre mim
- 🎯 Interesses: programação, Inteligência Artificial (IA)
- 🌱 Em constante aprendizado e curiosa por novas ferramentas
- 😄 Pronomes: ela/dela
- 💡 Objetivo: compartilhar projetos

<!-- Ícones/Badges -->
<div>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=csharp&logoColor=white" alt="C#"/>
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3"/>
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript"/>
  <img src="https://img.shields.io/badge/SQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="SQL"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5"/>
</div>

# Estatísticas
<div align="center">
  <img height="180em" src="https://github-readme-stats.vercel.app/api?username=yasmimfmacedo07&show_icons=true&theme=radical&hide_border=true&title_color=FF4D9D&icon_color=FF4D9D&text_color=ffffff&bg_color=0d1117" />
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=yasmimfmacedo07&layout=compact&theme=radical&hide_border=true&title_color=FF4D9D&text_color=ffffff&bg_color=0d1117" />
</div>

# COMPETÊNCIAS
- Fundamentos de redes
- Tipos de redes
- Crimpar
- Tipos de cabo
- Inglês técnico, leitura e interpretação de texto em inglês, escrita
- Aplicativos computacionais
- IA: Copilot, ChatGPT, Gemini, NotebookLM
- Normas ABNT
- Pacote office: Word, Excel, Power point
- Design Canva 
- Visual Studio 2022/2026
- Visual Studio Code 
- Github 
- Lógica de programação
- MySQL

<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Snake IA Auto</title>
  <style>
    :root {
      --bg-1: #081018;
      --bg-2: #111d2a;
      --panel: rgba(15, 22, 30, 0.9);
      --panel-border: rgba(148, 163, 184, 0.18);
      --text: #e5f0ff;
      --muted: #9ec0d9;
      --accent: #65f9c3;
      --accent-2: #2ee6b6;
      --danger: #ff6767;
      --board: #0d1420;
      --cell: rgba(148, 163, 184, 0.08);
      --snake-head: #7ef7d2;
      --snake-body: #41d9b0;
      --food: #ff5c8a;
    }

    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      height: 100%;
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      background:
        radial-gradient(circle at top, rgba(74, 222, 128, 0.18), transparent 30%),
        linear-gradient(180deg, var(--bg-1), var(--bg-2));
      color: var(--text);
    }

    body {
      display: grid;
      place-items: center;
      min-height: 100vh;
    }

    .wrapper {
      width: min(92vw, 560px);
      padding: 18px 18px 16px;
      border-radius: 22px;
      background: var(--panel);
      border: 1px solid var(--panel-border);
      box-shadow:
        0 30px 70px rgba(0, 0, 0, 0.48),
        inset 0 1px 0 rgba(255, 255, 255, 0.04);
      backdrop-filter: blur(10px);
    }

    .hud {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 14px;
      padding: 0 4px;
    }

    .title {
      font-size: 1.05rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      font-weight: 700;
    }

    .score-box {
      min-width: 120px;
      text-align: right;
      padding: 8px 12px;
      border-radius: 12px;
      background: rgba(101, 249, 195, 0.08);
      border: 1px solid rgba(101, 249, 195, 0.2);
      box-shadow: inset 0 0 16px rgba(101, 249, 195, 0.04);
    }

    .score-label {
      display: block;
      font-size: 0.68rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 3px;
    }

    .score-value {
      font-size: clamp(1.2rem, 2vw, 1.8rem);
      font-weight: 800;
      color: var(--accent);
    }

    canvas {
      width: 100%;
      height: auto;
      display: block;
      border-radius: 16px;
      background: linear-gradient(180deg, #0d1420, #0b111a);
      border: 1px solid rgba(148, 163, 184, 0.12);
      box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.3);
    }
  </style>
</head>
<body>
  <div class="wrapper">
    <div class="hud">
      <div class="title">Snake IA</div>
      <div class="score-box">
        <span class="score-label">Pontuação</span>
        <span class="score-value" id="score">0</span>
      </div>
    </div>
    <canvas id="game" width="432" height="432" aria-label="Jogo da cobra"></canvas>
  </div>

  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");
    const scoreEl = document.getElementById("score");

    const gridSize = 18;
    const cellSize = canvas.width / gridSize;
    const DIRS = [
      { x: 1, y: 0 },
      { x: -1, y: 0 },
      { x: 0, y: 1 },
      { x: 0, y: -1 }
    ];

    const state = {
      snake: [],
      food: { x: 0, y: 0 },
      direction: { x: 1, y: 0 },
      score: 0,
      gameOver: false,
      tickTimer: null
    };

    function keyOf(x, y) {
      return `${x},${y}`;
    }

    function randomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function clonePos(pos) {
      return { x: pos.x, y: pos.y };
    }

    function updateScore() {
      scoreEl.textContent = String(state.score);
    }

    function resetSnake() {
      state.snake = [
        { x: 8, y: 9 },
        { x: 7, y: 9 },
        { x: 6, y: 9 }
      ];
      state.direction = { x: 1, y: 0 };
    }

    function placeFood() {
      const occupied = new Set(state.snake.map(seg => keyOf(seg.x, seg.y)));
      const freeCells = [];

      for (let y = 0; y < gridSize; y++) {
        for (let x = 0; x < gridSize; x++) {
          if (!occupied.has(keyOf(x, y))) {
            freeCells.push({ x, y });
          }
        }
      }

      if (freeCells.length === 0) {
        return false;
      }

      const chosen = freeCells[randomInt(0, freeCells.length - 1)];
      state.food = { x: chosen.x, y: chosen.y };
      return true;
    }

    function resetGame() {
      clearInterval(state.tickTimer);
      state.score = 0;
      state.gameOver = false;
      resetSnake();
      placeFood();
      updateScore();
      draw();
      state.tickTimer = setInterval(gameStep, 120);
    }

    function isOccupied(cell, allowTailVacate) {
      for (let i = 0; i < state.snake.length; i++) {
        const seg = state.snake[i];
        if (seg.x === cell.x && seg.y === cell.y) {
          const isTail = i === state.snake.length - 1;
          if (isTail && allowTailVacate) {
            return false;
          }
          return true;
        }
      }
      return false;
    }

    function isMoveValid(nextHead, allowTailVacate) {
      if (nextHead.x < 0 || nextHead.y < 0 || nextHead.x >= gridSize || nextHead.y >= gridSize) {
        return false;
      }

      return !isOccupied(nextHead, allowTailVacate);
    }

    function manhattan(a, b) {
      return Math.abs(a.x - b.x) + Math.abs(a.y - b.y);
    }

    function shortestPathLength(start, target, allowTailVacate) {
      const queue = [clonePos(start)];
      const visited = new Set([keyOf(start.x, start.y)]);
      const distance = new Map([[keyOf(start.x, start.y), 0]]);

      while (queue.length > 0) {
        const current = queue.shift();
        if (current.x === target.x && current.y === target.y) {
          return distance.get(keyOf(current.x, current.y));
        }

        for (const dir of DIRS) {
          const next = { x: current.x + dir.x, y: current.y + dir.y };
          const nextKey = keyOf(next.x, next.y);

          if (next.x < 0 || next.y < 0 || next.x >= gridSize || next.y >= gridSize) {
            continue;
          }

          if (visited.has(nextKey)) {
            continue;
          }

          if (isOccupied(next, allowTailVacate)) {
            continue;
          }

          visited.add(nextKey);
          distance.set(nextKey, distance.get(keyOf(current.x, current.y)) + 1);
          queue.push(next);
        }
      }

      return Infinity;
    }

    function floodFillSafeCells(start, allowTailVacate) {
      const queue = [clonePos(start)];
      const visited = new Set([keyOf(start.x, start.y)]);
      let count = 0;

      while (queue.length > 0) {
        const current = queue.shift();
        count++;

        for (const dir of DIRS) {
          const next = { x: current.x + dir.x, y: current.y + dir.y };

          if (next.x < 0 || next.y < 0 || next.x >= gridSize || next.y >= gridSize) {
            continue;
          }

          const nextKey = keyOf(next.x, next.y);

          if (visited.has(nextKey)) {
            continue;
          }

          if (isOccupied(next, allowTailVacate)) {
            continue;
          }

          visited.add(nextKey);
          queue.push(next);
        }
      }

      return count;
    }

    function chooseAIMove() {
      const head = state.snake[0];
      const options = [];

      for (const dir of DIRS) {
        const nextHead = {
          x: head.x + dir.x,
          y: head.y + dir.y
        };

        const willEat = nextHead.x === state.food.x && nextHead.y === state.food.y;
        const allowTailVacate = !willEat;

        if (!isMoveValid(nextHead, allowTailVacate)) {
          continue;
        }

        const distanceToFood = manhattan(nextHead, state.food);
        const pathLength = shortestPathLength(nextHead, state.food, allowTailVacate);
        const safeCells = floodFillSafeCells(nextHead, allowTailVacate);

        options.push({
          dir,
          nextHead,
          willEat,
          distanceToFood,
          pathLength,
          safeCells
        });
      }

      if (options.length === 0) {
        return null;
      }

      options.sort((a, b) => {
        if (a.willEat !== b.willEat) {
          return a.willEat ? -1 : 1;
        }

        if (a.pathLength !== b.pathLength) {
          return a.pathLength - b.pathLength;
        }

        if (a.distanceToFood !== b.distanceToFood) {
          return a.distanceToFood - b.distanceToFood;
        }

        if (a.safeCells !== b.safeCells) {
          return b.safeCells - a.safeCells;
        }

        return 0;
      });

      return options[0].dir;
    }

    function triggerRestart() {
      state.gameOver = true;
      clearInterval(state.tickTimer);

      setTimeout(() => {
        resetGame();
      }, 1100);
    }

    function gameStep() {
      if (state.gameOver) {
        return;
      }

      const move = chooseAIMove();

      if (!move) {
        triggerRestart();
        return;
      }

      const head = state.snake[0];
      const nextHead = {
        x: head.x + move.x,
        y: head.y + move.y
      };

      const willEat = nextHead.x === state.food.x && nextHead.y === state.food.y;

      if (!isMoveValid(nextHead, !willEat)) {
        triggerRestart();
        return;
      }

      state.snake.unshift(nextHead);

      if (willEat) {
        state.score += 10;
        if (!placeFood()) {
          triggerRestart();
          return;
        }
      } else {
        state.snake.pop();
      }

      updateScore();
      draw();
    }

    function drawGrid() {
      ctx.fillStyle = "#0d1420";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      for (let y = 0; y < gridSize; y++) {
        for (let x = 0; x < gridSize; x++) {
          ctx.fillStyle = x % 2 === y % 2 ? "rgba(148,163,184,0.04)" : "rgba(148,163,184,0.015)";
          ctx.fillRect(x * cellSize, y * cellSize, cellSize, cellSize);
        }
      }
    }

    function drawFood() {
      const cx = state.food.x * cellSize + cellSize / 2;
      const cy = state.food.y * cellSize + cellSize / 2;
      const radius = cellSize * 0.34;

      ctx.beginPath();
      ctx.fillStyle = "#ff5c8a";
      ctx.arc(cx, cy, radius, 0, Math.PI * 2);
      ctx.fill();

      ctx.beginPath();
      ctx.fillStyle = "rgba(255,255,255,0.2)";
      ctx.arc(cx - radius * 0.32, cy - radius * 0.32, radius * 0.25, 0, Math.PI * 2);
      ctx.fill();
    }

    function drawSnake() {
      state.snake.forEach((seg, index) => {
        const x = seg.x * cellSize;
        const y = seg.y * cellSize;

        const isHead = index === 0;
        const padding = isHead ? 2 : 4;

        ctx.fillStyle = isHead ? "#7ef7d2" : "#41d9b0";
        ctx.fillRect(x + padding, y + padding, cellSize - padding * 2, cellSize - padding * 2);

        if (isHead) {
          ctx.fillStyle = "#0f172a";
          const eyeSize = cellSize * 0.09;
          const eyeOffset = cellSize * 0.18;

          const leftEyeX = x + cellSize * 0.38;
          const rightEyeX = x + cellSize * 0.66;
          const eyeY = y + cellSize * 0.38;

          ctx.fillRect(leftEyeX, eyeY, eyeSize, eyeSize);
          ctx.fillRect(rightEyeX, eyeY, eyeSize, eyeSize);
        }
      });
    }

    function draw() {
      drawGrid();
      drawFood();
      drawSnake();
    }

    resetGame();
  </script>
</body>
</html>
