
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Project By Alexander Nyarko</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #0f172a;
      --panel: #111827;
      --line: #374151;
      --x: #22d3ee;
      --o: #f472b6;
      --text: #e5e7eb;
      --accent: #10b981;
      --warning: #f59e0b;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      display: grid;
      place-items: center;
      background: radial-gradient(1200px 800px at 20% 0%, #0b1221 0%, var(--bg) 40%, #090f1d 100%);
      color: var(--text);
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif;
    }

    .game {
      width: 95%;
      max-width: 520px;
      background: linear-gradient(180deg, #0d1324 0%, var(--panel) 100%);
      border: 1px solid #1f2937;
      border-radius: 16px;
      padding: 18px;
      box-shadow:
        0 40px 80px rgba(0,0,0,0.5),
        inset 0 1px 0 rgba(255,255,255,0.04);
    }

    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 16px;
    }

    .title {
      font-weight: 700;
      letter-spacing: 0.4px;
    }

    .status {
      font-weight: 600;
      padding: 8px 12px;
      border-radius: 10px;
      background: #0b1221;
      border: 1px solid #1f2937;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      min-height: 38px;
    }

    .status .dot {
      width: 8px; height: 8px; border-radius: 50%;
      background: var(--accent);
      box-shadow: 0 0 0 4px rgba(16,185,129,0.12);
    }

    .controls {
      display: flex;
      gap: 10px;
      margin-top: 12px;
    }

    button {
      appearance: none;
      border: 1px solid #1f2937;
      background: #0d1324;
      color: var(--text);
      padding: 10px 14px;
      border-radius: 12px;
      font-weight: 600;
      cursor: pointer;
      transition: transform 120ms ease, background 120ms ease, border-color 120ms ease;
    }
    button:hover { transform: translateY(-1px); border-color: #334155; }
    button:active { transform: translateY(0); }

    .board {
      margin-top: 14px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      padding: 8px;
      border-radius: 16px;
      background: #0b1221;
      border: 1px solid #1f2937;
    }

    .cell {
      aspect-ratio: 1 / 1;
      font-size: clamp(36px, 8vw, 70px);
      font-weight: 800;
      letter-spacing: 1px;
      display: grid;
      place-items: center;
      background: #0a1322;
      border: 1px solid var(--line);
      border-radius: 14px;
      position: relative;
      user-select: none;
      outline: none;
    }
    .cell:hover { background: #0b1729; border-color: #415066; }
    .cell:disabled { cursor: default; opacity: 0.9; }

    .cell.x { color: var(--x); text-shadow: 0 0 20px rgba(34,211,238,0.25); }
    .cell.o { color: var(--o); text-shadow: 0 0 20px rgba(244,114,182,0.25); }

    .cell.win {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(16,185,129,0.18) inset, 0 0 24px rgba(16,185,129,0.22);
    }

    .panel {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-top: 14px;
    }

    .panel > div {
      background: #0b1221;
      border: 1px solid #1f2937;
      border-radius: 12px;
      padding: 10px 12px;
      display: grid;
      gap: 6px;
    }

    .label { font-size: 12px; color: #9ca3af; }
    .value { font-size: 18px; font-weight: 700; }

    .btn-secondary { background: #0b1221; }
    .btn-accent { background: #0e1a2c; border-color: #334155; }
    .btn-danger { background: #22120f; border-color: #3f1f16; color: #fca5a5; }
    .btn-danger:hover { border-color: #ef4444; background: #2a1411; }

    @media (prefers-reduced-motion: reduce) {
      button { transition: none; }
      .cell { transition: none; }
    }
  </style>
</head>
<body>
  <main class="game" aria-label="Tic Tac Toe">
    <div class="header">
      <div class="title">Tic Tac Toe By Alexander Nyarko</div>
      <div id="status" class="status" role="status" aria-live="polite">
        <span class="dot" aria-hidden="true"></span>
        <span id="statusText">Player X’s turn</span>
      </div>
    </div>

    <div id="board" class="board" role="grid" aria-label="3x3 tic tac toe board">
      <!-- 9 cells -->
      <button class="cell" data-index="0" role="gridcell" aria-label="Cell 1" aria-live="off"></button>
      <button class="cell" data-index="1" role="gridcell" aria-label="Cell 2" aria-live="off"></button>
      <button class="cell" data-index="2" role="gridcell" aria-label="Cell 3" aria-live="off"></button>
      <button class="cell" data-index="3" role="gridcell" aria-label="Cell 4" aria-live="off"></button>
      <button class="cell" data-index="4" role="gridcell" aria-label="Cell 5" aria-live="off"></button>
      <button class="cell" data-index="5" role="gridcell" aria-label="Cell 6" aria-live="off"></button>
      <button class="cell" data-index="6" role="gridcell" aria-label="Cell 7" aria-live="off"></button>
      <button class="cell" data-index="7" role="gridcell" aria-label="Cell 8" aria-live="off"></button>
      <button class="cell" data-index="8" role="gridcell" aria-label="Cell 9" aria-live="off"></button>
    </div>

    <div class="controls">
      <button id="restart" class="btn-accent">Restart round</button>
      <button id="swap" class="btn-secondary">Swap starting player</button>
      <button id="resetScores" class="btn-danger" title="Clear scores">Reset scores</button>
    </div>

    <div class="panel">
      <div>
        <div class="label">Current player</div>
        <div id="current" class="value">X</div>
      </div>
      <div>
        <div class="label">Score X</div>
        <div id="scoreX" class="value">0</div>
      </div>
      <div>
        <div class="label">Score O</div>
        <div id="scoreO" class="value">0</div>
      </div>
    </div>
  </main>

  <script>
    (function () {
      const cells = Array.from(document.querySelectorAll('.cell'));
      const statusText = document.getElementById('statusText');
      const currentEl = document.getElementById('current');
      const scoreXEl = document.getElementById('scoreX');
      const scoreOEl = document.getElementById('scoreO');
      const restartBtn = document.getElementById('restart');
      const swapBtn = document.getElementById('swap');
      const resetScoresBtn = document.getElementById('resetScores');

      const wins = [
        [0,1,2], [3,4,5], [6,7,8], // rows
        [0,3,6], [1,4,7], [2,5,8], // cols
        [0,4,8], [2,4,6]           // diags
      ];

      let board = Array(9).fill(null);
      let current = 'X';
      let starting = 'X';
      let score = { X: 0, O: 0 };
      let gameOver = false;

      function updateStatus(msg) {
        statusText.textContent = msg;
        currentEl.textContent = current;
      }

      function render() {
        cells.forEach((btn, i) => {
          const val = board[i];
          btn.textContent = val || '';
          btn.classList.toggle('x', val === 'X');
          btn.classList.toggle('o', val === 'O');
          btn.disabled = !!val || gameOver;
          btn.setAttribute('aria-label', `Cell ${i + 1}${val ? ' ' + val : ''}`);
        });
      }

      function checkWin() {
        for (const [a,b,c] of wins) {
          if (board[a] && board[a] === board[b] && board[b] === board[c]) {
            markWin([a,b,c]);
            return board[a];
          }
        }
        return null;
      }

      function markWin(indices) {
        indices.forEach(i => cells[i].classList.add('win'));
      }

      function checkDraw() {
        return board.every(v => v !== null);
      }

      function nextPlayer() {
        current = current === 'X' ? 'O' : 'X';
        updateStatus(`Player ${current}’s turn`);
      }

      function handleMove(index) {
        if (gameOver || board[index] !== null) return;

        board[index] = current;
        render();

        const winner = checkWin();
        if (winner) {
          gameOver = true;
          score[winner] += 1;
          scoreXEl.textContent = score.X;
          scoreOEl.textContent = score.O;
          updateStatus(`Player ${winner} wins!`);
          cells.forEach(btn => btn.disabled = true);
          return;
        }

        if (checkDraw()) {
          gameOver = true;
          updateStatus('It’s a draw.');
          return;
        }

        nextPlayer();
      }

      function restartRound() {
        board = Array(9).fill(null);
        gameOver = false;
        cells.forEach(btn => btn.classList.remove('win'));
        current = starting;
        render();
        updateStatus(`Player ${current}’s turn`);
      }

      function swapStarting() {
        starting = starting === 'X' ? 'O' : 'X';
        restartRound();
      }

      function resetScores() {
        score = { X: 0, O: 0 };
        scoreXEl.textContent = '0';
        scoreOEl.textContent = '0';
        restartRound();
      }

      // Events
      cells.forEach(btn => {
        btn.addEventListener('click', () => handleMove(Number(btn.dataset.index)));
        // Optional keyboard support: Enter/Space triggers click.
        btn.addEventListener('keydown', (e) => {
          if (e.key === 'Enter' || e.key === ' ') {
            e.preventDefault();
            btn.click();
          }
        });
      });

      restartBtn.addEventListener('click', restartRound);
      swapBtn.addEventListener('click', swapStarting);
      resetScoresBtn.addEventListener('click', resetScores);

      // Initial render
      render();
      updateStatus(`Player ${current}’s turn`);
    })();
  </script>
</body>
</html>


<!--
**phorenasarena-ship-it/phorenasarena-ship-it** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

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
