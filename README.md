# bacbo_site
<!DOCTYPE html>
<html>
<head>
  <title>Bac Bo Analyzer</title>
  <style>
    body {
      font-family: Arial;
      background: #0f172a;
      color: #fff;
      text-align: center;
    }
    h1 { color: #38bdf8; }
    button {
      padding: 12px;
      margin: 10px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .player { background: #22c55e; }
    .banker { background: #ef4444; }
    .box {
      margin-top: 20px;
      background: #1e293b;
      padding: 20px;
      border-radius: 10px;
    }
  </style>
</head>
<body>

<h1>📊 Bac Bo Analyzer PRO</h1>

<button class="player" onclick="add('P')">Player</button>
<button class="banker" onclick="add('B')">Banker</button>

<div class="box">
  <h2>Histórico</h2>
  <p id="historico"></p>

  <h2>Estatísticas</h2>
  <p id="stats"></p>

  <h2>Tendência</h2>
  <p id="tendencia"></p>
</div>

<script>
let historico = JSON.parse(localStorage.getItem('dados')) || [];

function add(r) {
  historico.push(r);
  localStorage.setItem('dados', JSON.stringify(historico));
  atualizar();
}

function atualizar() {
  document.getElementById("historico").innerText = historico.join(" - ");

  let p = historico.filter(x => x === 'P').length;
  let b = historico.filter(x => x === 'B').length;

  document.getElementById("stats").innerText =
    `Player: ${p} | Banker: ${b}`;

  let ult = historico.slice(-3);

  if (ult.every(x => x === 'P')) {
    document.getElementById("tendencia").innerText = "🔥 Tendência: Player";
  } else if (ult.every(x => x === 'B')) {
    document.getElementById("tendencia").innerText = "🔥 Tendência: Banker";
  } else {
    document.getElementById("tendencia").innerText = "⚖️ Sem tendência clara";
  }
}

atualizar();
</script>

</body>
</html>
