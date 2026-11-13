<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Game of Nim — Two-Player</title>
  <style>
    :root {
      --bg: #f4f6f9;
      --card: #ffffff;
      --text: #1e293b;
      --muted: #64748b;
      --p1: #2563eb;
      --p2: #db2777;
      --bean: #92400e;
      --bean-highlight: #b45309;
      --poison: #dc2626;
      --border: #e2e8f0;
    }

    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    body {
      margin: 0;
      padding: 2rem 1rem;
      background-color: var(--bg);
      color: var(--text);
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
    }

    .container {
      background: var(--card);
      max-width: 600px;
      width: 100%;
      padding: 2rem;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.06);
      border: 1px solid var(--border);
    }

    h1 {
      margin: 0 0 0.5rem;
      font-size: 1.75rem;
      text-align: center;
    }

    .subtitle {
      text-align: center;
      color: var(--muted);
      margin-bottom: 1.5rem;
      font-size: 0.95rem;
    }

    .mode-box {
      background: #f8fafc;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1rem;
      margin-bottom: 1.5rem;
    }

    .mode-box label {
      display: block;
      font-weight: 600;
      margin-bottom: 0.5rem;
      font-size: 0.9rem;
    }

    .mode-options {
      display: flex;
      gap: 0.75rem;
    }

    .mode-btn {
      flex: 1;
      padding: 0.6rem;
      border: 2px solid var(--border);
      background: #fff;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.85rem;
      transition: all 0.15s ease;
    }

    .mode-btn.active {
      border-color: #0f172a;
      background: #0f172a;
      color: #fff;
    }

    .mode-btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    .status-banner {
      text-align: center;
      padding: 0.9rem;
      border-radius: 10px;
      font-weight: 700;
      font-size: 1.1rem;
      margin-bottom: 1.5rem;
      transition: background-color 0.2s ease;
    }

    .turn-p1 {
      background: #dbeafe;
      color: var(--p1);
    }

    .turn-p2 {
      background: #fce7f3;
      color: var(--p2);
    }

    .winner-banner {
      background: #dcfce7;
      color: #15803d;
      font-size: 1.25rem;
    }

    .pile-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.75rem;
      font-weight: 600;
    }

    .pile-container {
      min-height: 150px;
      background: #fefce8;
      border: 2px dashed #fde047;
      border-radius: 12px;
      padding: 1.25rem;
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      justify-content: center;
      align-items: center;
      margin-bottom: 1.5rem;
    }

    .bean {
      width: 34px;
      height: 22px;
      background: radial-gradient(circle at 30% 30%, var(--bean-highlight), var(--bean));
      border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
      box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
      transition: transform 0.2s ease, opacity 0.2s ease;
    }

    .bean.poison-bean {
      background: radial-gradient(circle at 30% 30%, #f87171, var(--poison));
      box-shadow: 0 0 10px rgba(220, 38, 38, 0.5);
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 0.75rem;
      margin-bottom: 1.25rem;
    }

    .take-btn {
      padding: 0.9rem;
      font-size: 1rem;
      font-weight: 700;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      background: #0f172a;
      color: #fff;
      transition: transform 0.1s ease, background 0.15s ease;
    }

    .take-btn:hover:not(:disabled) {
      background: #334155;
      transform: translateY(-2px);
    }

    .take-btn:disabled {
      background: #cbd5e1;
      color: #94a3b8;
      cursor: not-allowed;
    }

    .reset-btn {
      width: 100%;
      padding: 0.75rem;
      background: transparent;
      border: 2px solid var(--border);
      border-radius: 10px;
      font-weight: 600;
      color: var(--muted);
      cursor: pointer;
      transition: all 0.15s ease;
    }

    .reset-btn:hover {
      border-color: var(--text);
      color: var(--text);
    }

    .log {
      margin-top: 1.5rem;
      border-top: 1px solid var(--border);
      padding-top: 1rem;
      font-size: 0.85rem;
      color: var(--muted);
      max-height: 120px;
      overflow-y: auto;
    }

    .log-entry {
      margin-bottom: 0.3rem;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Game of Nim</h1>
    <p class="subtitle">Take 1, 2, or 3 beans per turn from a single pile of 20.</p>

    <div class="mode-box">
      <label>Objective (Locked once the first move is made):</label>
      <div class="mode-options">
        <button id="modeNormal" class="mode-btn active" onclick="setMode('normal')">
          Normal Play (Last Bean Wins)
        </button>
        <button id="modeMisere" class="mode-btn" onclick="setMode('misere')">
          Misère / Poison (Last Bean Loses)
        </button>
      </div>
    </div>

    <div id="statusBanner" class="status-banner turn-p1">
      Player 1's Turn
    </div>

    <div class="pile-header">
      <span>Beans Remaining:</span>
      <span id="beanCount">20</span>
    </div>
    <div id="pileContainer" class="pile-container"></div>

    <div class="controls">
      <button id="btn1" class="take-btn" onclick="takeBeans(1)">Take 1</button>
      <button id="btn2" class="take-btn" onclick="takeBeans(2)">Take 2</button>
      <button id="btn3" class="take-btn" onclick="takeBeans(3)">Take 3</button>
    </div>

    <button class="reset-btn" onclick="resetGame()">Restart Game</button>

    <div id="moveLog" class="log"></div>
  </div>

  <script>
    const INITIAL_BEANS = 20;
    let beansRemaining = INITIAL_BEANS;
    let currentPlayer = 1;
    let gameMode = 'normal';
    let gameStarted = false;
    let gameOver = false;

    const statusBanner = document.getElementById('statusBanner');
    const beanCountEl = document.getElementById('beanCount');
    const pileContainer = document.getElementById('pileContainer');
    const moveLog = document.getElementById('moveLog');
    const modeNormalBtn = document.getElementById('modeNormal');
    const modeMisereBtn = document.getElementById('modeMisere');
    const takeButtons = [
      document.getElementById('btn1'),
      document.getElementById('btn2'),
      document.getElementById('btn3')
    ];

    function setMode(mode) {
      if (gameStarted) return;
      gameMode = mode;
      modeNormalBtn.classList.toggle('active', mode === 'normal');
      modeMisereBtn.classList.toggle('active', mode === 'misere');
      render();
    }

    function takeBeans(amount) {
      if (gameOver || amount > beansRemaining) return;

      if (!gameStarted) {
        gameStarted = true;
        modeNormalBtn.disabled = true;
        modeMisereBtn.disabled = true;
      }

      beansRemaining -= amount;
      logMove(`Player ${currentPlayer} took ${amount} bean${amount > 1 ? 's' : ''}. (${beansRemaining} left)`);

      if (beansRemaining === 0) {
        gameOver = true;
        const winner = gameMode === 'normal' ? currentPlayer : (currentPlayer === 1 ? 2 : 1);
        const reason = gameMode === 'normal'
          ? `Player ${currentPlayer} took the last bean and wins!`
          : `Player ${currentPlayer} took the poison bean! Player ${winner} wins!`;

        statusBanner.textContent = reason;
        statusBanner.className = 'status-banner winner-banner';
        logMove(`🏆 ${reason}`);
      } else {
        currentPlayer = currentPlayer === 1 ? 2 : 1;
        statusBanner.textContent = `Player ${currentPlayer}'s Turn`;
        statusBanner.className = `status-banner ${currentPlayer === 1 ? 'turn-p1' : 'turn-p2'}`;
      }

      render();
    }

    function render() {
      beanCountEl.textContent = beansRemaining;

      pileContainer.innerHTML = '';
      for (let i = 0; i < beansRemaining; i++) {
        const bean = document.createElement('div');
        bean.className = 'bean';
        if (gameMode === 'misere' && i === 0) {
          bean.classList.add('poison-bean');
          bean.title = 'Poison Bean (Last bean loses)';
        }
        pileContainer.appendChild(bean);
      }

      takeButtons.forEach((btn, index) => {
        const takeAmount = index + 1;
        btn.disabled = gameOver || takeAmount > beansRemaining;
      });
    }

    function logMove(text) {
      const entry = document.createElement('div');
      entry.className = 'log-entry';
      entry.textContent = text;
      moveLog.prepend(entry);
    }

    function resetGame() {
      beansRemaining = INITIAL_BEANS;
      currentPlayer = 1;
      gameStarted = false;
      gameOver = false;

      modeNormalBtn.disabled = false;
      modeMisereBtn.disabled = false;

      statusBanner.textContent = "Player 1's Turn";
      statusBanner.className = 'status-banner turn-p1';
      moveLog.innerHTML = '';

      render();
    }

    render();
  </script>
</body>
</html>
