<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>國中英語 U4 單字配對練習</title>
  <meta name="description" content="國中英語 U4 單字中英文配對練習，每次 10 題，可重複練習與錯題再練一次。">
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
      dis
