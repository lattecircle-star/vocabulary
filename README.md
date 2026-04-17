<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Unit 4 單字練習網站</title>
  <style>
    :root { --bg:#f4f7fb; --card:#fff; --text:#1f2937; --muted:#6b7280; --primary:#2563eb; --ok:#16a34a; --bad:#dc2626; --line:#dbe3ee; }
    * { box-sizing:border-box; }
    body { margin:0; font-family:Arial,'Noto Sans TC',sans-serif; background:var(--bg); color:var(--text); }
    .wrap { max-width:1120px; margin:0 auto; padding:24px; }
    .card { background:var(--card); border-radius:16px; padding:20px; box-shadow:0 8px 24px rgba(0,0,0,.08); margin-bottom:18px; }
    h1,h2,h3 { margin:0 0 12px; }
    .muted { color:var(--muted); }
    .controls { display:flex; gap:12px; flex-wrap:wrap; align-items:center; }
    button { border:none; border-radius:12px; padding:12px 18px; cursor:pointer; font-size:16px; font-weight:700; }
    .primary { background:var(--primary); color:#fff; }
    .secondary { background:#e5eefc; color:#1746a2; }
    .ghost { background:#eef2f7; color:#374151; }
    .pill { display:inline-block; padding:6px 10px; border-radius:999px; background:#eef2ff; color:#3730a3; font-size:14px; margin-right:8px; margin-bottom:8px; }
    .review-list { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:10px; }
    .word { border:1px solid var(--line); border-radius:12px; padding:12px; background:#fbfdff; }
    .hidden { display:none; }
    .topbar { display:flex; justify-content:space-between; gap:12px; flex-wrap:wrap; align-items:center; }
    .status { font-size:18px; font-weight:700; margin:10px 0 14px; }
    .grid { display:grid; grid-template-columns:1fr 1fr; gap:16px; }
    .col { border:1px solid var(--line); border-radius:14px; padding:14px; min-height:520px; background:#fafcff; }
    .item { border:2px solid var(--line); border-radius:12px; padding:12px; margin-bottom:10px; background:#fff; font-size:18px; text-align:left; width:100%; }
    .selected { border-color:var(--primary); background:#eff6ff; }
    .done { border-color:#bbf7d0; background:#f0fdf4; color:#166534; }
    .wrong { border-color:#fecaca; background:#fef2f2; }
    .qbox { border:1px solid var(--line); border-radius:14px; padding:18px; background:#fafcff; margin-bottom:16px; }
    .question { font-size:28px; font-weight:800; margin-bottom:14px; }
    .option-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; }
    .small { font-size:14px; }
    @media (max-width: 800px) { .grid,.option-grid { grid-template-columns:1fr; } .col { min-height:auto; } .question { font-size:24px; } }
  </style>
</head>
<body>
<div class="wrap">
  <div class="card">
    <h1>Unit 4 單字練習網站</h1>
    <p class="muted">可先複習全部單字，再選擇不同模式練習。每次 10 題，答錯的題目會再次出現。</p>
    <div class="controls">
      <button class="secondary" onclick="showReview()">先複習全部單字</button>
      <button class="primary" onclick="startPractice('match','part1')">配對練習 1-19</button>
      <button class="primary" onclick="startPractice('match','part2')">配對練習 20-38</button>
      <button class="primary" onclick="startPractice('mc_zh_to_en','part1')">中文選英文 1-19</button>
      <button class="primary" onclick="startPractice('mc_zh_to_en','part2')">中文選英文 20-38</button>
      <button class="primary" onclick="startPractice('mc_en_to_zh','part1')">英文選中文 1-19</button>
      <button class="primary" onclick="startPractice('mc_en_to_zh','part2')">英文選中文 20-38</button>
    </div>
  </div>

  <div id="reviewSection" class="card hidden">
    <div class="topbar"><h2>全部單字複習</h2><button class="ghost" onclick="hideReview()">關閉複習</button></div>
    <p><span class="pill">第 1 部分：1-19</span><span class="pill">第 2 部分：20-38</span></p>
    <div id="reviewList" class="review-list"></div>
  </div>

  <div id="matchSection" class="card hidden">
    <div class="topbar">
      <div><h2 id="matchTitle">配對練習</h2><p id="matchInfo" class="muted"></p></div>
      <div class="controls"><button class="secondary" onclick="restartCurrent()">再練一次這一部分</button><button class="ghost" onclick="showHome()">回首頁</button></div>
    </div>
    <div class="status" id="matchStatus"></div>
    <div class="grid">
      <div class="col"><h3>中文</h3><div id="leftCol"></div></div>
      <div class="col"><h3>English</h3><div id="rightCol"></div></div>
    </div>
  </div>

  <div id="mcSection" class="card hidden">
    <div class="topbar">
      <div><h2 id="mcTitle">選擇題練習</h2><p id="mcInfo" class="muted"></p></div>
      <div class="controls"><button class="secondary" onclick="restartCurrent()">再練一次這一部分</button><button class="ghost" onclick="showHome()">回首頁</button></div>
    </div>
    <div class="status" id="mcStatus"></div>
    <div class="qbox">
      <div id="questionText" class="question"></div>
      <div id="optionGrid" class="option-grid"></div>
    </div>
  </div>
</div>

<script>
const VOCAB = [
  {id:1, zh:'颱風', en:'typhoon'},
  {id:2, zh:'吹', en:'blow'},
  {id:3, zh:'玫瑰花', en:'rose'},
  {id:4, zh:'陽台', en:'balcony'},
  {id:5, zh:'必須；一定', en:'must'},
  {id:6, zh:'準備', en:'prepare'},
  {id:7, zh:'應該', en:'should'},
  {id:8, zh:'蠟燭', en:'candle'},
  {id:9, zh:'收音機', en:'radio'},
  {id:10, zh:'新聞；消息', en:'news'},
  {id:11, zh:'如果', en:'if'},
  {id:12, zh:'否則', en:'or'},
  {id:13, zh:'必須', en:'have to'},
  {id:14, zh:'熄滅', en:'go out'},
  {id:15, zh:'訓練', en:'train'},
  {id:16, zh:'面對', en:'face'},
  {id:17, zh:"盡力而為", en:"try one's best"},
  {id:18, zh:'打開（電源）', en:'turn on'},
  {id:19, zh:'最新的', en:'latest'},
  {id:20, zh:'星星', en:'star'},
  {id:21, zh:'閃耀；照耀', en:'shine'},
  {id:22, zh:'巨大的', en:'giant'},
  {id:23, zh:'浪', en:'wave'},
  {id:24, zh:'彩虹', en:'rainbow'},
  {id:25, zh:'漂亮的', en:'pretty'},
  {id:26, zh:'花園', en:'garden'},
  {id:27, zh:'青蛙', en:'frog'},
  {id:28, zh:'聲響；噪音', en:'noise'},
  {id:29, zh:'池塘', en:'pond'},
  {id:30, zh:'嘈雜的', en:'noisy'},
  {id:31, zh:'地震', en:'earthquake'},
  {id:32, zh:'勇敢地', en:'bravely'},
  {id:33, zh:'尖銳的', en:'sharp'},
  {id:34, zh:'到達', en:'reach'},
  {id:35, zh:'空間', en:'space'},
  {id:36, zh:'大小；尺寸', en:'size'},
  {id:37, zh:'作為；如同', en:'as'},
  {id:38, zh:'倍', en:'times'}
];

const PARTS = {
  part1: VOCAB.filter(v => v.id >= 1 && v.id <= 19),
  part2: VOCAB.filter(v => v.id >= 20 && v.id <= 38)
};

let currentMode = 'match';
let currentPart = 'part1';
let queue = [];
let wrongIds = new Set();
let roundNo = 1;
let currentBatch = [];
let matchedCount = 0;
let selectedLeft = null;
let selectedRight = null;
let mcIndex = 0;
let mcCorrect = 0;

function shuffle(arr) {
  const a = [...arr];
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

function showReview() {
  const sec = document.getElementById('reviewSection');
  const list = document.getElementById('reviewList');
  list.innerHTML = '';
  VOCAB.forEach(v => {
    const div = document.createElement('div');
    div.className = 'word';
    div.innerHTML = `<strong>${v.id}. ${v.zh}</strong><br><span class="muted">${v.en}</span>`;
    list.appendChild(div);
  });
  sec.classList.remove('hidden');
}

function hideReview() {
  document.getElementById('reviewSection').classList.add('hidden');
}

function showHome() {
  document.getElementById('matchSection').classList.add('hidden');
  document.getElementById('mcSection').classList.add('hidden');
}

function startPractice(mode, part) {
  currentMode = mode;
  currentPart = part;
  roundNo = 1;
  wrongIds = new Set();
  queue = shuffle(PARTS[part]);
  if (mode === 'match') nextMatchBatch();
  else nextMcBatch();
}

function restartCurrent() {
  startPractice(currentMode, currentPart);
}

function getBatch() {
  let batch = [];
  const wrongPool = shuffle(PARTS[currentPart].filter(v => wrongIds.has(v.id)));
  while (batch.length < 10 && wrongPool.length) {
    const item = wrongPool.shift();
    if (!batch.some(v => v.id === item.id)) batch.push(item);
  }
  while (batch.length < 10 && queue.length) {
    const item = queue.shift();
    if (!batch.some(v => v.id === item.id)) batch.push(item);
  }
  return batch;
}

function partLabel() {
  return currentPart === 'part1' ? '第 1 部分：1-19' : '第 2 部分：20-38';
}

function nextMatchBatch() {
  showHome();
  document.getElementById('matchSection').classList.remove('hidden');
  const batch = getBatch();

  if (batch.length === 0) {
    document.getElementById('matchTitle').textContent = partLabel() + ' 完成';
    document.getElementById('matchInfo').textContent = '太棒了！這一部分的單字都答對了。';
    document.getElementById('leftCol').innerHTML = '';
    document.getElementById('rightCol').innerHTML = '';
    document.getElementById('matchStatus').textContent = '全部完成';
    return;
  }

  currentBatch = batch;
  matchedCount = 0;
  selectedLeft = null;
  selectedRight = null;

  document.getElementById('matchTitle').textContent = '配對練習｜' + partLabel();
  document.getElementById('matchInfo').textContent = `第 ${roundNo} 回合，每次 10 題；答錯會再出現。`;
  renderMatchBatch();
  updateMatchStatus();
  roundNo++;
}

function renderMatchBatch() {
  const leftCol = document.getElementById('leftCol');
  const rightCol = document.getElementById('rightCol');
  leftCol.innerHTML = '';
  rightCol.innerHTML = '';

  shuffle(currentBatch).forEach(v => leftCol.appendChild(makeMatchBtn(v, 'left', `${v.id}. ${v.zh}`)));
  shuffle(currentBatch).forEach(v => rightCol.appendChild(makeMatchBtn(v, 'right', v.en)));
}

function makeMatchBtn(v, side, text) {
  const btn = document.createElement('button');
  btn.className = 'item';
  btn.textContent = text;
  btn.dataset.id = v.id;
  btn.dataset.side = side;
  btn.onclick = () => handleMatchPick(btn);
  return btn;
}

function handleMatchPick(btn) {
  if (btn.classList.contains('done')) return;
  const side = btn.dataset.side;
  if (side === 'left') {
    clearSelected('left');
    selectedLeft = btn;
    btn.classList.add('selected');
  } else {
    clearSelected('right');
    selectedRight = btn;
    btn.classList.add('selected');
  }
  if (selectedLeft && selectedRight) checkMatch();
}

function clearSelected(side) {
  document.querySelectorAll(`.item[data-side="${side}"]`).forEach(el => el.classList.remove('selected'));
}

function checkMatch() {
  const leftId = Number(selectedLeft.dataset.id);
  const rightId = Number(selectedRight.dataset.id);

  if (leftId === rightId) {
    selectedLeft.classList.remove('selected');
    selectedRight.classList.remove('selected');
    selectedLeft.classList.add('done');
    selectedRight.classList.add('done');
    selectedLeft.disabled = true;
    selectedRight.disabled = true;
    wrongIds.delete(leftId);
    matchedCount++;
  } else {
    selectedLeft.classList.add('wrong');
    selectedRight.classList.add('wrong');
    wrongIds.add(leftId);
    wrongIds.add(rightId);
    setTimeout(() => {
      selectedLeft?.classList.remove('wrong','selected');
      selectedRight?.classList.remove('wrong','selected');
    }, 500);
  }

  selectedLeft = null;
  selectedRight = null;
  updateMatchStatus();
  if (matchedCount === currentBatch.length) setTimeout(nextMatchBatch, 500);
}

function updateMatchStatus() {
  document.getElementById('matchStatus').textContent =
    `本回合已配對 ${matchedCount} / ${currentBatch.length} 題，待加強單字 ${wrongIds.size} 題`;
}

function nextMcBatch() {
  showHome();
  document.getElementById('mcSection').classList.remove('hidden');
  const batch = getBatch();

  if (batch.length === 0) {
    document.getElementById('mcTitle').textContent = partLabel() + ' 完成';
    document.getElementById('mcInfo').textContent = '太棒了！這一部分的單字都答對了。';
    document.getElementById('questionText').textContent = '全部完成';
    document.getElementById('optionGrid').innerHTML = '';
    document.getElementById('mcStatus').textContent = '全部完成';
    return;
  }

  currentBatch = shuffle(batch);
  mcIndex = 0;
  mcCorrect = 0;

  const modeName = currentMode === 'mc_zh_to_en' ? '中文選英文' : '英文選中文';
  document.getElementById('mcTitle').textContent = modeName + '｜' + partLabel();
  document.getElementById('mcInfo').textContent = `第 ${roundNo} 回合，每次 10 題；答錯會再出現。`;
  renderMcQuestion();
  updateMcStatus();
  roundNo++;
}

function renderMcQuestion() {
  const q = currentBatch[mcIndex];
  if (!q) {
    setTimeout(nextMcBatch, 400);
    return;
  }

  const optionGrid = document.getElementById('optionGrid');
  optionGrid.innerHTML = '';

  const pool = PARTS[currentPart].filter(v => v.id !== q.id);
  const distractors = shuffle(pool).slice(0, 3);
  const options = shuffle([q, ...distractors]);

  document.getElementById('questionText').textContent =
    currentMode === 'mc_zh_to_en' ? `${q.id}. ${q.zh}` : q.en;

  options.forEach(opt => {
    const btn = document.createElement('button');
    btn.className = 'item';
    btn.textContent = currentMode === 'mc_zh_to_en' ? opt.en : `${opt.id}. ${opt.zh}`;
    btn.onclick = () => checkMcAnswer(opt.id, q.id, btn);
    optionGrid.appendChild(btn);
  });
}

function checkMcAnswer(chosenId, answerId, btn) {
  const buttons = [...document.querySelectorAll('#optionGrid .item')];
  buttons.forEach(b => b.disabled = true);

  if (chosenId === answerId) {
    btn.classList.add('done');
    wrongIds.delete(answerId);
    mcCorrect++;
  } else {
    btn.classList.add('wrong');
    wrongIds.add(answerId);
    buttons.forEach(b => {
      const ans = currentBatch[mcIndex];
      const correctText = currentMode === 'mc_zh_to_en' ? ans.en : `${ans.id}. ${ans.zh}`;
      if (b.textContent === correctText) b.classList.add('done');
    });
  }

  updateMcStatus();
  mcIndex++;
  setTimeout(renderMcQuestion, 700);
}

function updateMcStatus() {
  document.getElementById('mcStatus').textContent =
    `目前第 ${Math.min(mcIndex + 1, currentBatch.length)} / ${currentBatch.length} 題，本回合答對 ${mcCorrect} 題，待加強單字 ${wrongIds.size} 題`;
}
</script>
</body>
</html>
