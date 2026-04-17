<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>單字中英文配對練習</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: "Noto Sans TC", Arial, sans-serif;
      margin: 0;
      background: #f4f7fb;
      color: #1f2937;
    }
    .container {
      max-width: 980px;
      margin: 30px auto;
      padding: 20px;
    }
    .card {
      background: #fff;
      border-radius: 16px;
      padding: 24px;
      box-shadow: 0 8px 24px rgba(0,0,0,.08);
      margin-bottom: 20px;
    }
    h1, h2, h3 { margin-top: 0; }
    .topbar {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      align-items: center;
      justify-content: space-between;
    }
    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 16px;
    }
    button {
      border: none;
      border-radius: 10px;
      padding: 10px 16px;
      cursor: pointer;
      font-size: 16px;
      background: #2563eb;
      color: white;
    }
    button:hover { opacity: .92; }
    button.secondary { background: #64748b; }
    button.success { background: #16a34a; }
    button.warning { background: #ea580c; }
    select {
      padding: 10px 12px;
      border-radius: 10px;
      border: 1px solid #cbd5e1;
      font-size: 16px;
    }
    .hidden { display: none; }
    .review-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 12px;
      margin-top: 16px;
    }
    .word-item {
      border: 1px solid #e5e7eb;
      border-radius: 12px;
      padding: 12px;
      background: #f8fafc;
    }
    .word-item b {
      display: block;
      font-size: 18px;
      color: #0f172a;
      margin-bottom: 6px;
    }
    .question {
      border: 1px solid #dbeafe;
      background: #f8fbff;
      border-radius: 14px;
      padding: 16px;
      margin-bottom: 16px;
    }
    .question h3 {
      margin-bottom: 12px;
      font-size: 18px;
    }
    .options {
      display: grid;
      gap: 10px;
    }
    label.option {
      display: block;
      padding: 10px 12px;
      border: 1px solid #cbd5e1;
      border-radius: 10px;
      background: white;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      padding: 16px;
      border-radius: 12px;
      background: #f1f5f9;
    }
    .correct { color: #15803d; font-weight: bold; }
    .wrong { color: #b91c1c; font-weight: bold; }
    .muted { color: #64748b; }
    .score {
      font-size: 22px;
      font-weight: bold;
      color: #1d4ed8;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="card">
      <div class="topbar">
        <div>
          <h1>單字中英文配對練習</h1>
          <p class="muted">每次隨機出 10 題，可重複練習，先複習再作答。</p>
        </div>
        <div>
          <label for="groupSelect">選擇範圍：</label>
          <select id="groupSelect">
            <option value="1">第 1 部分（1-19）</option>
            <option value="2">第 2 部分（20-38）</option>
          </select>
        </div>
      </div>

      <div class="controls">
        <button class="secondary" onclick="showReview()">全部複習</button>
        <button class="success" onclick="startQuiz()">開始 10 題練習</button>
        <button class="warning" onclick="startQuiz()">重新出題</button>
      </div>
    </div>

    <div id="reviewSection" class="card hidden">
      <h2>單字複習</h2>
      <div id="reviewList" class="review-grid"></div>
    </div>

    <div id="quizSection" class="card hidden">
      <h2>10 題配對練習</h2>
      <form id="quizForm"></form>
      <div class="controls">
        <button type="button" onclick="submitQuiz()">送出答案</button>
        <button type="button" class="warning" onclick="startQuiz()">再練一次</button>
      </div>
      <div id="resultSection" class="result hidden"></div>
    </div>
  </div>

  <script>
    const words = [
      { no: 1, en: "apple", zh: "蘋果" },
      { no: 2, en: "banana", zh: "香蕉" },
      { no: 3, en: "cat", zh: "貓" },
      { no: 4, en: "dog", zh: "狗" },
      { no: 5, en: "book", zh: "書" },
      { no: 6, en: "chair", zh: "椅子" },
      { no: 7, en: "table", zh: "桌子" },
      { no: 8, en: "school", zh: "學校" },
      { no: 9, en: "teacher", zh: "老師" },
      { no: 10, en: "student", zh: "學生" },
      { no: 11, en: "water", zh: "水" },
      { no: 12, en: "bread", zh: "麵包" },
      { no: 13, en: "milk", zh: "牛奶" },
      { no: 14, en: "house", zh: "房子" },
      { no: 15, en: "car", zh: "汽車" },
      { no: 16, en: "sun", zh: "太陽" },
      { no: 17, en: "moon", zh: "月亮" },
      { no: 18, en: "flower", zh: "花" },
      { no: 19, en: "tree", zh: "樹" },

      { no: 20, en: "bird", zh: "鳥" },
      { no: 21, en: "fish", zh: "魚" },
      { no: 22, en: "egg", zh: "蛋" },
      { no: 23, en: "rice", zh: "米飯" },
      { no: 24, en: "happy", zh: "快樂的" },
      { no: 25, en: "sad", zh: "傷心的" },
      { no: 26, en: "big", zh: "大的" },
      { no: 27, en: "small", zh: "小的" },
      { no: 28, en: "fast", zh: "快的" },
      { no: 29, en: "slow", zh: "慢的" },
      { no: 30, en: "red", zh: "紅色" },
      { no: 31, en: "blue", zh: "藍色" },
      { no: 32, en: "green", zh: "綠色" },
      { no: 33, en: "yellow", zh: "黃色" },
      { no: 34, en: "morning", zh: "早上" },
      { no: 35, en: "night", zh: "晚上" },
      { no: 36, en: "friend", zh: "朋友" },
      { no: 37, en: "family", zh: "家人" },
      { no: 38, en: "picture", zh: "圖片" }
    ];

    let currentQuestions = [];

    function getSelectedGroupWords() {
      const group = document.getElementById("groupSelect").value;
      return group === "1"
        ? words.filter(w => w.no >= 1 && w.no <= 19)
        : words.filter(w => w.no >= 20 && w.no <= 38);
    }

    function shuffle(array) {
      const arr = [...array];
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    function showReview() {
      const reviewSection = document.getElementById("reviewSection");
      const reviewList = document.getElementById("reviewList");
      const selectedWords = getSelectedGroupWords();

      reviewList.innerHTML = selectedWords.map(word => `
        <div class="word-item">
          <b>${word.no}. ${word.en}</b>
          <span>${word.zh}</span>
        </div>
      `).join("");

      reviewSection.classList.remove("hidden");
    }

    function startQuiz() {
      const selectedWords = getSelectedGroupWords();
      const quizWords = shuffle(selectedWords).slice(0, 10);
      currentQuestions = quizWords;

      const quizForm = document.getElementById("quizForm");
      const quizSection = document.getElementById("quizSection");
      const resultSection = document.getElementById("resultSection");

      resultSection.classList.add("hidden");
      resultSection.innerHTML = "";

      quizForm.innerHTML = quizWords.map((word, index) => {
        const wrongChoices = shuffle(
          selectedWords.filter(w => w.zh !== word.zh)
        ).slice(0, 3).map(w => w.zh);

        const options = shuffle([word.zh, ...wrongChoices]);

        return `
          <div class="question">
            <h3>第 ${index + 1} 題：<span style="color:#1d4ed8">${word.en}</span> 的中文是？</h3>
            <div class="options">
              ${options.map(option => `
                <label class="option">
                  <input type="radio" name="q${index}" value="${option}">
                  ${option}
                </label>
              `).join("")}
            </div>
          </div>
        `;
      }).join("");

      quizSection.classList.remove("hidden");
      window.scrollTo({ top: quizSection.offsetTop - 20, behavior: "smooth" });
    }

    function submitQuiz() {
      let score = 0;
      let output = "";

      currentQuestions.forEach((word, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const answer = selected ? selected.value : "未作答";
        const isCorrect = answer === word.zh;

        if (isCorrect) score++;

        output += `
          <p>
            第 ${index + 1} 題：${word.en} → 正確答案是「${word.zh}」；
            你的答案是「${answer}」：
            <span class="${isCorrect ? 'correct' : 'wrong'}">
              ${isCorrect ? '答對' : '答錯'}
            </span>
          </p>
        `;
      });

      const resultSection = document.getElementById("resultSection");
      resultSection.innerHTML = `
        <p class="score">你的分數：${score} / 10</p>
        ${output}
      `;
      resultSection.classList.remove("hidden");
      window.scrollTo({ top: resultSection.offsetTop - 20, behavior: "smooth" });
    }
  </script>
</body>
</html>
