<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>國中英語 U4 單字配對練習</title>
  <style>
    :root{
      --bg:#eef4ff;
      --card:#ffffff;
      --line:#d9e3f0;
      --text:#1f2937;
      --sub:#64748b;
      --primary:#2563eb;
      --primary-dark:#1d4ed8;
      --green:#16a34a;
      --orange:#ea580c;
      --purple:#7c3aed;
      --gray:#64748b;
      --good:#15803d;
      --bad:#b91c1c;
    }

    *{ box-sizing:border-box; }

    body{
      margin:0;
      font-family:"Noto Sans TC","Microsoft JhengHei",Arial,sans-serif;
      background:linear-gradient(180deg,#eef4ff 0%,#f8fbff 100%);
      color:var(--text);
    }

    .wrap{
      max-width:1100px;
      margin:0 auto;
      padding:20px;
    }

    .card{
      background:var(--card);
      border:1px solid var(--line);
      border-radius:20px;
      box-shadow:0 10px 30px rgba(37,99,235,.08);
      padding:22px;
      margin:18px 0;
    }

    h1,h2,h3,p{ margin-top:0; }

    .title{
      display:flex;
      justify-content:space-between;
      align-items:flex-start;
      gap:16px;
      flex-wrap:wrap;
    }

    .subtitle{
      color:var(--sub);
      margin-bottom:0;
    }

    .toolbar{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
      gap:12px;
      margin-top:18px;
    }

    .field{
      display:flex;
      flex-direction:column;
      gap:8px;
    }

    label{
      font-weight:600;
    }

    select{
      width:100%;
      padding:12px 14px;
      border-radius:12px;
      border:1px solid #cbd5e1;
      font-size:16px;
      background:#fff;
    }

    .buttons{
      display:flex;
      flex-wrap:wrap;
      gap:10px;
      margin-top:16px;
    }

    button{
      border:none;
      border-radius:14px;
      padding:13px 18px;
      font-size:16px;
      font-weight:700;
      cursor:pointer;
      color:#fff;
      background:var(--primary);
      min-height:48px;
    }

    button:hover{
      filter:brightness(.97);
    }

    button:disabled{
      opacity:.55;
      cursor:not-allowed;
    }

    .btn-gray{ background:var(--gray); }
    .btn-green{ background:var(--green); }
    .btn-orange{ background:var(--orange); }
    .btn-purple{ background:var(--purple); }

    .pill{
      display:inline-block;
      padding:6px 12px;
      border-radius:999px;
      background:#dbeafe;
      color:#1d4ed8;
      font-size:14px;
      font-weight:700;
      margin-top:10px;
    }

    .hidden{ display:none; }

    .review-grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
      gap:12px;
      margin-top:16px;
    }

    .word-item{
      border:1px solid var(--line);
      border-radius:14px;
      padding:14px;
      background:#f8fbff;
    }

    .word-item .num{
      color:var(--primary-dark);
      font-weight:700;
      font-size:14px;
      margin-bottom:6px;
    }

    .word-item .main{
      font-size:20px;
      font-weight:800;
      margin-bottom:6px;
    }

    .word-item .sub{
      color:var(--sub);
      font-size:16px;
    }

    .quiz-top{
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:14px;
    }

    .progress{
      color:var(--sub);
      font-weight:700;
    }

    .question{
      border:1px solid #cfe0ff;
      background:#f8fbff;
      border-radius:16px;
      padding:18px;
      margin-bottom:16px;
    }

    .question-title{
      font-size:19px;
      font-weight:800;
      margin-bottom:12px;
      line-height:1.5;
    }

    .ask-word{
      color:var(--primary-dark);
    }

    .options{
      display:grid;
      gap:10px;
    }

    .option{
      display:flex;
      align-items:center;
      gap:10px;
      border:1px solid #cbd5e1;
      border-radius:14px;
      padding:12px 14px;
      background:#fff;
      cursor:pointer;
      transition:.15s ease;
    }

    .option:hover{
      border-color:#93c5fd;
      background:#f8fbff;
    }

    .option input{
      transform:scale(1.2);
      accent-color:var(--primary);
    }

    .result{
      margin-top:18px;
      background:#f8fafc;
      border:1px solid var(--line);
      border-radius:16px;
      padding:18px;
    }

    .score{
      font-size:26px;
      font-weight:900;
      color:var(--primary-dark);
      margin-bottom:10px;
    }

    .good{ color:var(--good); font-weight:800; }
    .bad{ color:var(--bad); font-weight:800; }

    .result-item{
      padding:10px 0;
      border-bottom:1px dashed #cbd5e1;
      line-height:1.7;
    }

    .result-item:last-child{
      border-bottom:none;
    }

    .footer-note{
      color:var(--sub);
      font-size:14px;
      margin-top:8px;
    }

    .status-box{
      margin-top:12px;
      padding:12px 14px;
      border-radius:12px;
      background:#f5f3ff;
      border:1px solid #ddd6fe;
      color:#5b21b6;
      font-weight:700;
    }

    @media (max-width: 700px){
      .wrap{ padding:14px; }
      .card{ padding:16px; border-radius:16px; }
      h1{ font-size:24px; }
      .question-title{ font-size:18px; }
      button{ width:100%; }
      .buttons{
        display:grid;
        grid-template-columns:1fr;
      }
    }
  </style>
</head>
<body>
  <div class="wrap">
    <section class="card">
      <div class="title">
        <div>
          <h1>國中英語 U4 單字配對練習</h1>
          <p class="subtitle">每次 10 題、隨機出題、可重複練習，也可只重練錯題。</p>
          <div class="pill" id="currentInfo">目前範圍：第 1 部分（1-19）｜模式：英文選中文</div>
        </div>
      </div>

      <div class="toolbar">
        <div class="field">
          <label for="groupSelect">練習範圍</label>
          <select id="groupSelect" onchange="updateInfo()">
            <option value="1">第 1 部分（1-19）</option>
            <option value="2">第 2 部分（20-38）</option>
          </select>
        </div>

        <div class="field">
          <label for="modeSelect">作答模式</label>
          <select id="modeSelect" onchange="updateInfo()">
            <option value="en2zh">英文選中文</option>
            <option value="zh2en">中文選英文</option>
          </select>
        </div>
      </div>

      <div class="buttons">
        <button class="btn-gray" onclick="showReview()">全部複習</button>
        <button class="btn-green" onclick="startQuiz()">開始 10 題練習</button>
        <button class="btn-orange" onclick="startQuiz()">重新出題</button>
      </div>
    </section>

    <section id="reviewSection" class="card hidden">
      <h2>全部複習</h2>
      <p class="subtitle">先看完本範圍全部單字，再開始練習。</p>
      <div id="reviewList" class="review-grid"></div>
    </section>

    <section id="quizSection" class="card hidden">
      <div class="quiz-top">
        <h2>單字測驗</h2>
        <div class="progress" id="progressText">共 10 題</div>
      </div>

      <div id="statusBox" class="status-box hidden"></div>
      <form id="quizForm"></form>

      <div class="buttons">
        <button type="button" onclick="submitQuiz()">送出答案</button>
        <button type="button" class="btn-orange" onclick="startQuiz()">再練一次</button>
        <button type="button" class="btn-purple" id="retryWrongBtn" onclick="retryWrongQuestions()" disabled>錯題再練一次</button>
      </div>

      <div id="resultSection" class="result hidden"></div>
    </section>
  </div>

  <script>
    const words = [
      { no: 1, zh: "颱風", en: "typhoon" },
      { no: 2, zh: "吹", en: "blow" },
      { no: 3, zh: "玫瑰花", en: "rose" },
      { no: 4, zh: "陽台", en: "balcony" },
      { no: 5, zh: "必須；一定", en: "must" },
      { no: 6, zh: "準備", en: "prepare" },
      { no: 7, zh: "應該", en: "should" },
      { no: 8, zh: "蠟燭", en: "candle" },
      { no: 9, zh: "收音機", en: "radio" },
      { no: 10, zh: "新聞；消息", en: "news" },
      { no: 11, zh: "如果", en: "if" },
      { no: 12, zh: "否則", en: "or" },
      { no: 13, zh: "必須", en: "have to" },
      { no: 14, zh: "熄滅", en: "go out" },
      { no: 15, zh: "訓練", en: "train" },
      { no: 16, zh: "面對", en: "face" },
      { no: 17, zh: "盡力而為", en: "try one's best" },
      { no: 18, zh: "打開（電源）", en: "turn on" },
      { no: 19, zh: "最新的", en: "latest" },
      { no: 20, zh: "星星", en: "star" },
      { no: 21, zh: "閃耀；照耀", en: "shine" },
      { no: 22, zh: "巨大的", en: "giant" },
      { no: 23, zh: "浪", en: "wave" },
      { no: 24, zh: "彩虹", en: "rainbow" },
      { no: 25, zh: "漂亮的", en: "pretty" },
      { no: 26, zh: "花園", en: "garden" },
      { no: 27, zh: "青蛙", en: "frog" },
      { no: 28, zh: "聲響；噪音", en: "noise" },
      { no: 29, zh: "池塘", en: "pond" },
      { no: 30, zh: "嘈雜的", en: "noisy" },
      { no: 31, zh: "地震", en: "earthquake" },
      { no: 32, zh: "勇敢地", en: "bravely" },
      { no: 33, zh: "尖銳的", en: "sharp" },
      { no: 34, zh: "到達", en: "reach" },
      { no: 35, zh: "空間", en: "space" },
      { no: 36, zh: "大小；尺寸", en: "size" },
      { no: 37, zh: "作為；如同", en: "as" },
      { no: 38, zh: "倍", en: "times" }
    ];

    let currentQuestions = [];
    let wrongQuestions = [];
    let quizSourceType = "normal";

    function shuffle(array) {
      const arr = [...array];
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    function getSelectedGroupWords() {
      const group = document.getElementById("groupSelect").value;
      return group === "1"
        ? words.filter(w => w.no >= 1 && w.no <= 19)
        : words.filter(w => w.no >= 20 && w.no <= 38);
    }

    function updateInfo() {
      const group = document.getElementById("groupSelect").value;
      const mode = document.getElementById("modeSelect").value;
      const groupText = group === "1" ? "第 1 部分（1-19）" : "第 2 部分（20-38）";
      const modeText = mode === "en2zh" ? "英文選中文" : "中文選英文";
      document.getElementById("currentInfo").textContent =
        `目前範圍：${groupText}｜模式：${modeText}`;
    }

    function showReview() {
      const selectedWords = getSelectedGroupWords();
      const mode = document.getElementById("modeSelect").value;
      const reviewList = document.getElementById("reviewList");

      reviewList.innerHTML = selectedWords.map(word => `
        <div class="word-item">
          <div class="num">第 ${word.no} 字</div>
          <div class="main">${mode === "en2zh" ? word.en : word.zh}</div>
          <div class="sub">${mode === "en2zh" ? word.zh : word.en}</div>
        </div>
      `).join("");

      document.getElementById("reviewSection").classList.remove("hidden");
      window.scrollTo({ top: document.getElementById("reviewSection").offsetTop - 20, behavior: "smooth" });
    }

    function buildQuestion(word, index, selectedWords, mode) {
      const isEnToZh = mode === "en2zh";
      const ask = isEnToZh ? word.en : word.zh;
      const correct = isEnToZh ? word.zh : word.en;
      const poolKey = isEnToZh ? "zh" : "en";

      const wrongChoices = shuffle(
        selectedWords.filter(w => w.no !== word.no)
      ).slice(0, 3).map(w => w[poolKey]);

      const options = shuffle([correct, ...wrongChoices]);

      return `
        <div class="question">
          <div class="question-title">
            第 ${index + 1} 題：<span class="ask-word">${ask}</span> 的${isEnToZh ? "中文" : "英文"}是？
          </div>
          <div class="options">
            ${options.map(option => `
              <label class="option">
                <input type="radio" name="q${index}" value="${escapeHtml(option)}">
                <span>${option}</span>
              </label>
            `).join("")}
          </div>
        </div>
      `;
    }

    function renderQuiz(questionSet, sourceType = "normal") {
      const selectedWords = getSelectedGroupWords();
      const mode = document.getElementById("modeSelect").value;
      currentQuestions = shuffle(questionSet);
      quizSourceType = sourceType;

      document.getElementById("quizForm").innerHTML = currentQuestions
        .map((word, index) => buildQuestion(word, index, selectedWords, mode))
        .join("");

      document.getElementById("progressText").textContent = `共 ${currentQuestions.length} 題`;

      const statusBox = document.getElementById("statusBox");
      if (sourceType === "wrong") {
        statusBox.textContent = `目前是錯題重練，共 ${currentQuestions.length} 題。`;
        statusBox.classList.remove("hidden");
      } else {
        statusBox.classList.add("hidden");
        statusBox.textContent = "";
      }

      document.getElementById("resultSection").classList.add("hidden");
      document.getElementById("resultSection").innerHTML = "";
      document.getElementById("quizSection").classList.remove("hidden");

      window.scrollTo({ top: document.getElementById("quizSection").offsetTop - 20, behavior: "smooth" });
    }

    function startQuiz() {
      const selectedWords = getSelectedGroupWords();
      const questionSet = shuffle(selectedWords).slice(0, 10);
      renderQuiz(questionSet, "normal");
    }

    function submitQuiz() {
      const mode = document.getElementById("modeSelect").value;
      const isEnToZh = mode === "en2zh";
      let score = 0;
      let resultHtml = "";
      wrongQuestions = [];

      currentQuestions.forEach((word, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const userAnswer = selected ? selected.value : "未作答";
        const correct = isEnToZh ? word.zh : word.en;
        const ask = isEnToZh ? word.en : word.zh;
        const isCorrect = userAnswer === correct;

        if (isCorrect) {
          score++;
        } else {
          wrongQuestions.push(word);
        }

        resultHtml += `
          <div class="result-item">
            第 ${index + 1} 題：${ask} → 正確答案是「${correct}」；你的答案是「${userAnswer}」：
            <span class="${isCorrect ? "good" : "bad"}">${isCorrect ? "答對" : "答錯"}</span>
          </div>
        `;
      });

      const retryBtn = document.getElementById("retryWrongBtn");
      retryBtn.disabled = wrongQuestions.length =
