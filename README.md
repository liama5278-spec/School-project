<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Game of Nim — 1P vs Clanker & 2P</title>
  <style>
    :root {
      --bg: #f4f6f9;
      --card: #ffffff;
      --text: #1e293b;
      --muted: #64748b;
      --p1: #2563eb;
      --p2: #db2777;
      --bot: #7c3aed;
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
      max-width: 620px;
      width: 100%;
      padding: 2rem;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.06);
      border: 1px solid var(--border);
    }

    h1 {
      margin: 0 0 0.4rem;
      font-size: 1.75rem;
      text-align: center;
    }

    .subtitle {
      text-align: center;
      color: var(--muted);
      margin-bottom: 1.5rem;
      font-size: 0.95rem;
    }

    .settings-box {
      background: #f8fafc;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1rem;
      margin-bottom: 1.25rem;
      display: flex;
      flex-direction: column;
      gap: 0.9rem;
    }

    .setting-group label {
      display: block;
      font-weight: 600;
      margin-bottom: 0.4rem;
      font-size: 0.85rem;
      color: var(--text);
    }

    .option-row {
      display: flex;
      gap: 0.6rem;
    }

    .opt-btn {
      flex: 1;
      padding: 0.55rem 0.75rem;
      border: 2px solid var(--border);
      background: #fff;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.85rem;
      transition: all 0.15s ease;
    }

    .opt-btn.active {
      border-color: #0f172a;
      background: #0f172a;
      color: #fff;
    }

    .opt-btn:disabled {
      opacity: 0.55;
      cursor: not-allowed;
    }

    .bot-options {
      display: none;
      flex-direction: column;
      gap: 0.9rem;
      padding-top: 0.5rem;
      border-top: 1px dashed var(--border);
    }

    .bot-options.visible {
      display: flex;
    }

    .status-banner {
      text-align: center;
      padding: 0.9rem;
      border-radius: 10px;
      font-weight: 700;
      font-size: 1.1rem;
      margin-bottom: 1.25rem;
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

    .turn-bot {
      background: #ede9fe;
      color: var(--bot);
    }

    .winner-banner {
      background: #dcfce7;
      color: #15803d;
      font-size: 1.15rem;
    }

    .loser-banner {
      background: #fee2e2;
      color: #b91c1c;
      font-size: 1.15rem;
    }

    .pile-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.6rem;
      font-weight: 600;
    }

    .pile-container {
      min-height: 145px;
      background: #fefce8;
      border: 2px dashed #fde047;
      border-radius: 12px;
      padding: 1.25rem;
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      justify-content: center;
      align-items: center;
      margin-bottom: 1.25rem;
    }

    .bean {
      width: 34px;
      height: 22px;
      background: radial-gradient(circle at 30% 30%, var(--bean-highlight), var(--bean));
      border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
      box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
      transition: transform 0.2s ease;
    }

    .bean.poison-bean {
      background: radial-gradient(circle at 30% 30%, #f87171, var(--poison));
      box-shadow: 0 0 10px rgba(220, 38, 38, 0.5);
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 0.75rem;
      margin-bottom: 1rem;
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
      margin-top: 1.25rem;
      border-top: 1px solid var(--border);
      padding-top: 0.9rem;
      font-size: 0.85rem;
      color: var(--muted);
      max-height: 130px;
      overflow-y: auto;
    }

    .log-entry {
      margin-bottom: 0.35rem;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Game of Nim</h1>
    <p class="subtitle">Take 1, 2, or 3 beans per turn from a single pile of 20.</p>

    <div class="settings-box">
      <!-- Opponent Mode -->
      <div class="setting-group">
        <label>Players:</label>
        <div class="option-row">
          <button id="opp2P" class="opt-btn active" onclick="setOpponent('2p')">2-Player Local</button>
          <button id="oppBot" class="opt-btn" onclick="setOpponent('bot')">1P vs Clanker Bot 🤖</button>
        </div>
      </div>

      <!-- Bot-Specific Options -->
      <div id="botOptions" class="bot-options">
        <div class="setting-group">
          <label>Clanker Intelligence:</label>
          <div class="option-row">
            <button id="diffCasual" class="opt-btn active" onclick="setDifficulty('casual')">Casual Clanker</button>
            <button id="diffSmart" class="opt-btn" onclick="setDifficulty('smart')">Unbeatable AI</button>
          </div>
        </div>
        <div class="setting-group">
          <label>Who Goes First:</label>
          <div class="option-row">
            <button id="firstHuman" class="opt-btn active" onclick="setFirstTurn('human')">You Go First</button>
            <button id="firstBot" class="opt-btn" onclick="setFirstTurn('bot')">Clanker Goes First</button>
          </div>
        </div>
      </div>

      <!-- Win Objective -->
      <div class="setting-group">
        <label>Objective (Locked once play begins):</label>
        <div class="option-row">
          <button id="modeNormal" class="opt-btn active" onclick="setMode('normal')">Normal (Last Wins)</button>
          <button id="modeMisere" class="opt-btn" onclick="setMode('misere')">Misère / Poison (Last Loses)</button>
        </div>
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
      <button id="btn1" class="take-btn" onclick="handleHumanMove(1)">Take 1</button>
      <button id="btn2" class="take-btn" onclick="handleHumanMove(2)">Take 2</button>
      <button id="btn3" class="take-btn" onclick="handleHumanMove(3)">Take 3</button>
    </div>

    <button class="reset-btn" onclick="resetGame()">Restart Game</button>

    <div id="moveLog" class="log"></div>
  </div>

  <script>
    const INITIAL_BEANS = 20;
    let beansRemaining = INITIAL_BEANS;
    let currentPlayer = 1; // 1 = Player 1 / Human, 2 = Player 2 / Clanker
    let opponentType = '2p'; // '2p' or 'bot'
    let botDifficulty = 'casual'; // 'casual' or 'smart'
    let firstTurn = 'human'; // 'human' or 'bot'
    let gameMode = 'normal'; // 'normal' or 'misere'
    let gameStarted = false;
    let gameOver = false;
    let botThinking = false;
    let botTimer = null;

    const statusBanner = document.getElementById('statusBanner');
    const beanCountEl = document.getElementById('beanCount');
    const pileContainer = document.getElementById('pileContainer');
    const moveLog = document.getElementById('moveLog');
    const botOptionsEl = document.getElementById('botOptions');

    const settingButtons = [
      document.getElementById('opp2P'),
      document.getElementById('oppBot'),
      document.getElementById('diffCasual'),
      document.getElementById('diffSmart'),
      document.getElementById('firstHuman'),
      document.getElementById('firstBot'),
      document.getElementById('modeNormal'),
      document.getElementById('modeMisere')
    ];

    const takeButtons = [
      document.getElementById('btn1'),
      document.getElementById('btn2'),
      document.getElementById('btn3')
    ];

    function setOpponent(type) {
      if (gameStarted) return;
      opponentType = type;
      document.getElementById('opp2P').classList.toggle('active', type === '2p');
      document.getElementById('oppBot').classList.toggle('active', type === 'bot');
      botOptionsEl.classList.toggle('visible', type === 'bot');
      resetGame();
    }

    function setDifficulty(diff) {
      if (gameStarted) return;
      botDifficulty = diff;
      document.getElementById('diffCasual').classList.toggle('active', diff === 'casual');
      document.getElementById('diffSmart').classList.toggle('active', diff === 'smart');
    }

    function setFirstTurn(who) {
      if (gameStarted) return;
      firstTurn = who;
      document.getElementById('firstHuman').classList.toggle('active', who === 'human');
