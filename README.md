<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Timer Tapis Roulant 0–5K</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    :root {
      --bg: #050816;
      --card: #0b1020;
      --running-grad: linear-gradient(135deg, #22c55e, #14b8a6);
      --walk-grad: linear-gradient(135deg, #f97316, #ec4899);
      --text-main: #f9fafb;
      --text-muted: #9ca3af;
      --accent: #38bdf8;
      --danger: #ef4444;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #1e293b 0, #020617 55%, #000 100%);
      color: var(--text-main);
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 16px;
    }
    .app {
      width: 100%;
      max-width: 420px;
      background: rgba(15, 23, 42, 0.92);
      border-radius: 16px;
      box-shadow: 0 24px 60px rgba(15, 23, 42, 0.8);
      padding: 16px 18px 20px;
      border: 1px solid rgba(148, 163, 184, 0.25);
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
    }
    .title {
      font-size: 18px;
      font-weight: 700;
      letter-spacing: 0.03em;
    }
    .badge {
      font-size: 11px;
      padding: 4px 8px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.6);
      color: var(--text-muted);
      text-transform: uppercase;
    }
    .controls {
      display: flex;
      gap: 6px;
      margin-bottom: 12px;
      flex-wrap: wrap;
    }
    select {
      flex: 1;
      min-width: 100px;
      padding: 6px 10px;
      border-radius: 8px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      background: rgba(15, 23, 42, 0.85);
      color: var(--text-main);
      font-size: 13px;
      cursor: pointer;
    }
    select:focus {
      outline: none;
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.1);
    }
    .phase-card {
      border-radius: 18px;
      padding: 16px 14px;
      margin-bottom: 12px;
      position: relative;
      overflow: hidden;
    }
    .phase-running {
      background-image: var(--running-grad);
    }
    .phase-walk {
      background-image: var(--walk-grad);
    }
    .phase-label {
      font-size: 14px;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      opacity: 0.9;
    }
    .time {
      font-size: 52px;
      font-weight: 700;
      margin: 6px 0 4px;
    }
    .details {
      font-size: 14px;
      opacity: 0.95;
    }
    .subdetails {
      font-size: 12px;
      opacity: 0.85;
      margin-top: 4px;
    }
    .chips {
      display: flex;
      gap: 6px;
      margin-top: 8px;
      flex-wrap: wrap;
    }
    .chip {
      font-size: 11px;
      padding: 3px 8px;
      border-radius: 999px;
      background: rgba(15, 23, 42, 0.2);
      border: 1px solid rgba(15, 23, 42, 0.25);
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }
    .chip-dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: var(--text-main);
      opacity: 0.9;
    }
    .info-row {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 12px;
    }
    .buttons {
      display: flex;
      gap: 8px;
      margin-bottom: 4px;
    }
    button {
      flex: 1;
      border-radius: 999px;
      border: none;
      font-size: 15px;
      font-weight: 600;
      padding: 10px 0;
      cursor: pointer;
      transition: transform 0.08s ease, box-shadow 0.08s ease, opacity 0.2s;
    }
    button:active {
      transform: translateY(1px) scale(0.98);
      box-shadow: none;
    }
    button:disabled {
      opacity: 0.4;
      cursor: default;
      transform: none;
    }
    .btn-primary {
      background: var(--accent);
      color: #020617;
      box-shadow: 0 12px 30px rgba(56, 189, 248, 0.35);
    }
    .btn-secondary {
      background: rgba(15, 23, 42, 1);
      color: var(--text-main);
      border: 1px solid rgba(148, 163, 184, 0.4);
    }
    .btn-danger {
      background: rgba(239, 68, 68, 0.1);
      color: var(--danger);
      border: 1px solid rgba(248, 113, 113, 0.6);
    }
    .hint {
      font-size: 11px;
      color: var(--text-muted);
      text-align: center;
      margin-top: 2px;
    }
  </style>
</head>
<body>

<div class="app">
  <header>
    <div class="title">0–5K Tapis Timer</div>
    <div class="badge" id="badge">Week 1 · Run 1</div>
  </header>

  <div class="controls">
    <select id="weekSelect" onchange="updateWorkout()">
      <option value="W1">Settimana 1</option>
      <option value="W2">Settimana 2</option>
      <option value="W3">Settimana 3</option>
      <option value="W4">Settimana 4</option>
      <option value="W5">Settimana 5</option>
      <option value="W6">Settimana 6</option>
      <option value="W7">Settimana 7</option>
      <option value="W8">Settimana 8</option>
      <option value="W9">Settimana 9</option>
      <option value="W10">Settimana 10</option>
    </select>
    <select id="sessionSelect" onchange="updateWorkout()">
      <option value="A1">Allenamento 1</option>
      <option value="A2">Allenamento 2</option>
    </select>
  </div>

  <div id="phaseCard" class="phase-card phase-walk">
    <div id="phaseLabel" class="phase-label">Premi START</div>
    <div id="time" class="time">00:00</div>
    <div id="details" class="details">—</div>
    <div id="subdetails" class="subdetails">Prossimo: —</div>
    <div class="chips">
      <div class="chip">
        <span class="chip-dot"></span>
        <span id="chipStep">Step 0 di 0</span>
      </div>
      <div class="chip">
        <span class="chip-dot"></span>
        <span id="chipBlock">—</span>
      </div>
    </div>
  </div>

  <div class="info-row">
    <div id="totalTime">Totale: ~25 min</div>
    <div id="status">Pronto</div>
  </div>

  <div class="buttons">
    <button id="startBtn" class="btn-primary">Start</button>
    <button id="pauseBtn" class="btn-secondary" disabled>Pausa</button>
    <button id="resetBtn" class="btn-danger" disabled>Reset</button>
  </div>
  <div class="hint">Tip: appoggia il telefono sul tappeto e segui velocità e pendenza sul display.</div>
</div>

<script>
  const workoutData = {
    W1: {
      A1: {
        total: "~25 min",
        description: "(1' corsa / 2' camminata) × 6",
        intervals: [
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      },
      A2: {
        total: "~25 min",
        description: "(1' corsa / 2' camminata) × 7",
        intervals: [
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 60, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      }
    },
    W2: {
      A1: {
        total: "~25 min",
        description: "(90\" corsa / 2' camminata) × 6",
        intervals: [
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      },
      A2: {
        total: "~28 min",
        description: "(90\" corsa / 2' camminata) × 7",
        intervals: [
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 90, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      }
    },
    W3: {
      A1: {
        total: "~28 min",
        description: "(2' corsa / 2' camminata) × 6",
        intervals: [
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 120, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      },
      A2: {
        total: "~30 min",
        description: "(3' corsa / 2' camminata) × 5",
        intervals: [
          { label: "Corsa", seconds: 180, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 180, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 180, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 180, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 180, speed: 7.0, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      }
    },
    W4: {
      A1: {
        total: "~30 min",
        description: "(4' corsa / 2' camminata) × 4",
        intervals: [
          { label: "Corsa", seconds: 240, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 240, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 240, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 240, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      },
      A2: {
        total: "~32 min",
        description: "(5' corsa / 2' camminata) × 4",
        intervals: [
          { label: "Corsa", seconds: 300, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 300, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 300, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 300, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      }
    },
    W5: {
      A1: {
        total: "~30 min",
        description: "(6' corsa / 2' camminata) × 3",
        intervals: [
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      },
      A2: {
        total: "~32 min",
        description: "(8' corsa / 2' camminata) × 3",
        intervals: [
          { label: "Corsa", seconds: 480, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 480, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 480, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 }
        ]
      }
    },
    W6: {
      A1: {
        total: "~28 min",
        description: "(6' corsa 1% + 2' camminata 2%) × 3",
        intervals: [
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 2 },
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 2 },
          { label: "Corsa", seconds: 360, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 2 }
        ]
      },
      A2: {
        total: "~30 min",
        description: "10' corsa + 2' camminata + 10' corsa",
        intervals: [
          { label: "Corsa", seconds: 600, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 600, speed: 7.5, incline: 1 }
        ]
      }
    },
    W7: {
      A1: {
        total: "~32 min",
        description: "12' corsa + 2' camminata + 12' corsa",
        intervals: [
          { label: "Corsa", seconds: 720, speed: 7.5, incline: 1 },
          { label: "Camminata", seconds: 120, speed: 5.0, incline: 1 },
          { label: "Corsa", seconds: 720, speed: 7.5, incline: 1 }
        ]
      },
      A2: {
        total: "~30 min",
        description: "20' corsa continua",
        intervals: [
          { label: "Corsa", seconds: 1200, speed: 7.5, incline: 1 }
        ]
      }
    },
    W8: {
      A1: {
        total: "~32 min",
        description: "22' corsa continua",
        intervals: [
          { label: "Corsa", seconds: 1320, speed: 7.5, incline: 1 }
        ]
      },
      A2: {
        total: "~35 min",
        description: "25' corsa continua",
        intervals: [
          { label: "Corsa", seconds: 1500, speed: 7.5, incline: 1 }
        ]
      }
    },
    W9: {
      A1: {
        total: "~35 min",
        description: "28' corsa continua",
        intervals: [
          { label: "Corsa", seconds: 1680, speed: 7.5, incline: 1 }
        ]
      },
      A2: {
        total: "~26 min",
        description: "fino a 4 km (corsa continua)",
        intervals: [
          { label: "Corsa", seconds: 1560, speed: 7.5, incline: 1 }
        ]
      }
    },
    W10: {
      A1: {
        total: "~30 min",
        description: "fino a 4.5 km (corsa continua)",
        intervals: [
          { label: "Corsa", seconds: 1800, speed: 7.5, incline: 1 }
        ]
      },
      A2: {
        total: "~33 min",
        description: "fino a 5 km (corsa continua)",
        intervals: [
          { label: "Corsa", seconds: 2000, speed: 7.5, incline: 1 }
        ]
      }
    }
  };

  let currentInterval = [];
  let currentIndex = 0;
  let remaining = 0;
  let timerId = null;
  let running = false;
  let started = false;

  const phaseCard = document.getElementById('phaseCard');
  const phaseLabel = document.getElementById('phaseLabel');
  const timeEl = document.getElementById('time');
  const detailsEl = document.getElementById('details');
  const subdetailsEl = document.getElementById('subdetails');
  const chipStep = document.getElementById('chipStep');
  const chipBlock = document.getElementById('chipBlock');
  const statusEl = document.getElementById('status');
  const badgeEl = document.getElementById('badge');
  const totalTimeEl = document.getElementById('totalTime');
  const weekSelect = document.getElementById('weekSelect');
  const sessionSelect = document.getElementById('sessionSelect');

  const startBtn = document.getElementById('startBtn');
  const pauseBtn = document.getElementById('pauseBtn');
  const resetBtn = document.getElementById('resetBtn');

  function formatTime(sec) {
    const m = String(Math.floor(sec / 60)).padStart(2, '0');
    const s = String(sec % 60).padStart(2, '0');
    return m + ":" + s;
  }

  function updateWorkout() {
    const week = weekSelect.value;
    const session = sessionSelect.value;
    const workout = workoutData[week][session];

    currentInterval = workout.intervals;
    currentIndex = 0;
    remaining = 0;
    running = false;
    started = false;

    if (timerId !== null) {
      clearInterval(timerId);
      timerId = null;
    }

    const weekNum = week.replace('W', '');
    const sessionNum = session.replace('A', '');
    badgeEl.textContent = "Week " + weekNum + " · Run " + sessionNum;
    totalTimeEl.textContent = "Totale: " + workout.total;
    chipBlock.textContent = workout.description;

    phaseCard.classList.remove('phase-running');
    phaseCard.classList.add('phase-walk');
    phaseLabel.textContent = "Premi START";
    timeEl.textContent = "00:00";
    detailsEl.textContent = "—";
    subdetailsEl.textContent = "Prossimo: —";
    chipStep.textContent = "Step 0 di 0";
    statusEl.textContent = "Pronto";

    startBtn.disabled = false;
    pauseBtn.disabled = true;
    resetBtn.disabled = true;
  }

  function updatePhaseCard() {
    if (currentIndex >= currentInterval.length) {
      phaseCard.classList.remove('phase-walk');
      phaseCard.classList.add('phase-running');
      phaseLabel.textContent = "Fatto!";
      timeEl.textContent = "00:00";
      detailsEl.textContent = "Cammina defaticando 5–10 minuti";
      subdetailsEl.textContent = "Hai completato questo allenamento";
      chipStep.textContent = "Step " + currentInterval.length + " di " + currentInterval.length;
      statusEl.textContent = "Completato";
      return;
    }

    const step = currentInterval[currentIndex];
    const totalSteps = currentInterval.length;
    const stepNum = currentIndex + 1;

    if (step.label === "Corsa") {
      phaseCard.classList.remove('phase-walk');
      phaseCard.classList.add('phase-running');
    } else {
      phaseCard.classList.remove('phase-running');
      phaseCard.classList.add('phase-walk');
    }

    phaseLabel.textContent = step.label;
    timeEl.textContent = formatTime(remaining);
    detailsEl.textContent = step.speed.toFixed(1) + " km/h · " + step.incline + "% pendenza";

    if (currentIndex + 1 < currentInterval.length) {
      const next = currentInterval[currentIndex + 1];
      subdetailsEl.textContent =
        "Prossimo: " + next.label + " " +
        next.speed.toFixed(1) + " km/h · " + next.incline + "%";
    } else {
      subdetailsEl.textContent = "Prossimo: fine allenamento";
    }

    chipStep.textContent = "Step " + stepNum + " di " + totalSteps;
  }

  function nextInterval() {
    currentIndex++;
    if (currentIndex >= currentInterval.length) {
      clearInterval(timerId);
      timerId = null;
      running = false;
      startBtn.disabled = true;
      pauseBtn.disabled = true;
      resetBtn.disabled = false;
      updatePhaseCard();
      return;
    }
    remaining = currentInterval[currentIndex].seconds;
    updatePhaseCard();
  }

  function tick() {
    if (!running) return;
    remaining--;
    if (remaining <= 0) {
      nextInterval();
    } else {
      timeEl.textContent = formatTime(remaining);
    }
  }

  startBtn.onclick = function () {
    if (!started) {
      started = true;
      currentIndex = 0;
      remaining = currentInterval[0].seconds;
      updatePhaseCard();
      timerId = setInterval(tick, 1000);
    }
    running = true;
    startBtn.disabled = true;
    pauseBtn.disabled = false;
    resetBtn.disabled = false;
    statusEl.textContent = "In corso";
  };

  pauseBtn.onclick = function () {
    running = false;
    startBtn.disabled = false;
    pauseBtn.disabled = true;
    statusEl.textContent = "In pausa";
  };

  resetBtn.onclick = function () {
    updateWorkout();
  };

  updateWorkout();
</script>

</body>
</html>
