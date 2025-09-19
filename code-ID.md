---
layout: base
title: LxD Game
permalink: /CodeID
comments: true
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Code Identify Game</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #9797d4ff;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
      justify-content: center;
      align-items: center;
    }
    .game-container {
      background: #ffffffff;
      border-radius: 12px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.08);
      padding: 2rem 2.5rem;
      margin-top: 2rem;
      min-width: 350px;
      max-width: 90vw;
    }
    .code-block {
      background: #222;
      color: #e0e0e0;
      border-radius: 8px;
      padding: 1.2rem;
      font-size: 1.1rem;
      font-family: 'Fira Mono', 'Consolas', monospace;
      margin-bottom: 2rem;
      white-space: pre-wrap;
      word-break: break-word;
    }
    .options-bar {
      display: flex;
      gap: 1rem;
      justify-content: center;
      margin-bottom: 1rem;
    }
    .option-btn {
      background: #9c99ccff;
      color: #eae8f5ff;
      border: none;
      border-radius: 6px;
      padding: 0.7rem 1.5rem;
      font-size: 1rem;
      cursor: pointer;
      transition: background 0.2s, transform 0.06s;
    }
    .option-btn:hover {
      background: #9c99ccff;
      transform: translateY(-1px);
    }
    .result-message {
      text-align: center;
      font-size: 1.1rem;
      margin-top: 0.5rem;
      min-height: 1.5em;
    }
    .correct { color: #2e8b57; font-weight: bold; }
    .incorrect { color: #c0392b; font-weight: bold; }
    .next-btn {
      margin-top: 1.2rem;
      background: #9d5663ff;
      color: #fff;
      border: none;
      border-radius: 8px;
      padding: 0.85rem 2.2rem;
      font-size: 1.15rem;
      font-weight: 700;
      cursor: pointer;
      display: none;
      opacity: 0;
      transition: opacity 0.3s, background 0.2s, transform 0.15s;
      box-shadow: 0 2px 12px rgba(76,64,101,0.10);
    }
    .next-btn.show {
      display: inline-block !important;
      opacity: 1;
      animation: fadeInNext 0.4s;
    }
    .next-btn:hover {
      background: #b86b7bff;
      transform: scale(1.06);
    }
    @keyframes fadeInNext {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .level-btn { position: fixed; right: 1rem; background: #e3b1d9ff; color: #571d2aff; border: none; padding: 0.6rem 0.9rem; border-radius: 6px; cursor: pointer; box-shadow: 0 2px 8px rgba(0,0,0,0.12); font-size: 1rem; z-index: 10; transition: background 0.2s, color 0.2s, transform 0.12s; }
    .level-btn.level2 { top: 6rem; }
    .level-btn.level3 { top: 8.5rem; }
    .level-btn.active { font-weight: 700; transform: scale(1.06); }
  </style>
</head>
<body>
  <button id="level2Btn" class="level-btn level2">Level Two</button>
  <button id="level3Btn" class="level-btn level3">Level Three</button>

  <div class="game-container start-aesthetic" id="startScreen">
    <h1>Welcome to Code Identify!</h1>
    <ul>
      <li>• Test your skills by matching code snippets to their language.</li>
      <li>• Each round, a code snippet appears.</li>
      <li>• Choose the correct language from the options.</li>
      <li>• Try to get as many correct as you can!</li>
    </ul>
    <button id="startBtn">Start Game</button>
  </div>

  <div id="game-container">
    <button id="toggleStatsBtn">Show Stats</button>
    <div id="stats-container" style="display:none;"></div>
    <div class="game-container" id="gameContainer" style="display:none;">
      <div id="progressBarContainer">
        <div>Progress: <span id="progressText">0 / 15</span></div>
        <div style="background:#c2c2e2ff; border-radius:8px; width:100%; height:18px; overflow:hidden;">
          <div id="progressBar" style="background:linear-gradient(90deg,#9797d4 60%,#4c4065 100%); height:100%; width:0%; border-radius:8px;"></div>
        </div>
      </div>
      <h2>Code Identify Game</h2>
      <div class="code-block" id="codeBlock">Loading...</div>
      <div class="options-bar" id="optionsBar"></div>
      <div class="result-message" id="resultMessage"></div>
      <button class="next-btn" id="nextBtn">Next</button>
    </div>
  </div>

  <div class="game-container start-aesthetic" id="levelCompleteScreen" style="display:none;">
    <h2 id="levelCompleteTitle">Level Complete!</h2>
    <p id="levelCompleteMsg"></p>
    <button id="nextLevelBtn">Go to Next Level</button>
  </div>

  <!-- Level 3 Explanation Box -->
  <div id="explanationBox" style="display:none; position:fixed; right:1rem; top:50%; transform:translateY(-50%); background:#3498db; color:white; padding:1rem; border-radius:8px; max-width:250px; font-size:0.95rem; z-index:20;"></div>

  <script>
    const codeSnippets = [
      { code: "body {\n  background: #222;\n  color: #fff;\n}", lang: 'CSS' },
      { code: "function greet(name) {\n  return 'Hello, ' + name + '!';\n}", lang: 'Javascript' },
      { code: "def add(a, b):\n    return a + b", lang: 'Python' },
      { code: "# Markdown example\n- item 1\n- item 2", lang: 'Markdown' },
      { code: "<h1>Hello</h1>\n<p>HTML here</p>", lang: 'HTML' }
    ];
    const languages = ['CSS','Javascript','Python','Markdown','HTML'];
    const levelThreeSnippets = [
      { code: "fetch('/api/data').then(res=>res.json()).then(d=>console.log(d));", lang:'Javascript' },
      { code: "a,b=0,1\nfor _ in range(n):\n    a,b=b,a+b\nreturn a", lang:'Python' },
      { code: "<section><article><h2>Title</h2></article></section>", lang:'HTML' }
    ];

    let currentSnippet = null;
    let advancedMode = false;
    let levelThreeMode = false;
    let currentLevel = 1;
    let correctCount = 0;
    const languageStats = {};
    languages.forEach(lang=>languageStats[lang]={correct:0,incorrect:0});

    function getRandomSnippet() {
      if(levelThreeMode) return levelThreeSnippets[Math.floor(Math.random()*levelThreeSnippets.length)];
      return codeSnippets[Math.floor(Math.random()*codeSnippets.length)];
    }

    function sanitizeForAdvanced(code){ return code.replace(/\b(JavaScript|Javascript|Python|HTML|CSS|Markdown)\b/gi,'').trim(); }

    function renderOptions() {
      const optionsBar = document.getElementById('optionsBar');
      optionsBar.innerHTML='';
      languages.forEach(lang=>{
        const btn=document.createElement('button');
        btn.className='option-btn';
        btn.textContent=lang;
        btn.onclick=()=>checkAnswer(lang);
        optionsBar.appendChild(btn);
      });
    }

    function updateProgressBar() {
      const pct=Math.min(100,Math.round((correctCount/15)*100));
      document.getElementById('progressBar').style.width=pct+'%';
      document.getElementById('progressText').textContent=`${correctCount} / 15`;
    }

    function resetProgress() { correctCount=0; updateProgressBar(); }

    function showSnippet() {
      currentSnippet=getRandomSnippet();
      let displayCode=currentSnippet.code;
      if(advancedMode||levelThreeMode) displayCode=sanitizeForAdvanced(displayCode);
      document.getElementById('codeBlock').textContent=displayCode;
      document.getElementById('resultMessage').textContent='';
      document.getElementById('nextBtn').classList.remove('show');
      renderOptions();
    }

    function checkAnswer(selected){
      const result=document.getElementById('resultMessage');
      const correctLanguage=currentSnippet.lang;
      if(selected===correctLanguage){
        result.textContent='Correct!';
        result.className='result-message correct';
        document.getElementById('nextBtn').classList.add('show');
        correctCount++;
        updateProgressBar();
        languageStats[correctLanguage].correct++;
        if(correctCount>=15)setTimeout(showLevelComplete,500);
      } else {
        result.textContent='Try again!';
        result.className='result-message incorrect';
        languageStats[selected].incorrect++;
      }

      // Level 3 explanation box
      if(currentLevel===3){
        const box=document.getElementById('explanationBox');
        let explanation=`<strong>Correct:</strong> ${correctLanguage}<br>`;
        switch(correctLanguage){
          case 'Python': explanation+='Python uses indentation and "def" for functions.'; break;
          case 'Javascript': explanation+='JavaScript uses functions or console.log.'; break;
          case 'HTML': explanation+='HTML uses tags like <h1>, <p>, <ul>.'; break;
          case 'CSS': explanation+='CSS styles elements using selectors and properties.'; break;
          case 'Markdown': explanation+='Markdown uses symbols like *, **, #, - for formatting.'; break;
        }
        box.innerHTML=explanation;
        box.style.display='block';
        document.getElementById('nextBtn').onclick=()=>{
          box.style.display='none';
          showSnippet();
        };
      } else {
        document.getElementById('nextBtn').onclick=showSnippet;
      }

      updateStatsDisplay();
    }

    function updateStatsDisplay(){
      let statsHtml='<h3>Language Stats</h3><table><tr><th>Lang</th><th>Correct</th><th>Incorrect</th></tr>';
      languages.forEach(lang=>{
        statsHtml+=`<tr><td>${lang}</td><td>${languageStats[lang].correct}</td><td>${languageStats[lang].incorrect}</td></tr>`;
      });
      statsHtml+='</table>';
      document.getElementById('stats-container').innerHTML=statsHtml;
    }

    document.getElementById('startBtn').onclick=()=>{
      document.getElementById('startScreen').style.display='none';
      document.getElementById('gameContainer').style.display='block';
      currentLevel=1; resetProgress(); updateStatsDisplay(); showSnippet();
    };

    document.getElementById('nextLevelBtn').onclick=()=>{
      document.getElementById('levelCompleteScreen').style.display='none';
      document.getElementById('gameContainer').style.display='block';
      resetProgress();
      currentLevel++;
      if(currentLevel===2){ advancedMode=true; level2Btn.classList.add('active'); levelThreeMode=false; level3Btn.classList.remove('active'); }
      if(currentLevel===3){ levelThreeMode=true; level3Btn.classList.add('active'); advancedMode=true; level2Btn.classList.remove('active'); }
      showSnippet();
    };

    document.getElementById('toggleStatsBtn').onclick=()=>{
      const stats=document.getElementById('stats-container');
      if(stats.style.display==='none'){ stats.style.display='block'; this.textContent='Hide Stats'; } 
      else { stats.style.display='none'; this.textContent='Show Stats'; }
    };

    level2Btn.addEventListener('click',()=>{
      if(levelThreeMode){ levelThreeMode=false; level3Btn.classList.remove('active'); }
      advancedMode=!advancedMode;
      level2Btn.classList.toggle('active',advancedMode);
      showSnippet();
    });

    level3Btn.addEventListener('click',()=>{
      levelThreeMode=!levelThreeMode;
      if(levelThreeMode){ advancedMode=true; level2Btn.classList.remove('active'); }
      level3Btn.classList.toggle('active',levelThreeMode);
      showSnippet();
    });

    window.onload=()=>{
      document.getElementById('startScreen').style.display='flex';
      document.getElementById('gameContainer').style.display='none';
      document.getElementById('levelCompleteScreen').style.display='none';
      currentLevel=1; resetProgress(); updateStatsDisplay();
    };

    function showLevelComplete(){
      document.getElementById('gameContainer').style.display='none';
      document.getElementById('levelCompleteScreen').style.display='flex';
      if(currentLevel===1){ document.getElementById('levelCompleteTitle').textContent='Level 1 Complete!'; document.getElementById('levelCompleteMsg').innerHTML='You answered 15 questions correctly!<br>Click below to go to Level 2.'; document.getElementById('nextLevelBtn').style.display='inline-block'; }
      if(currentLevel===2){ document.getElementById('levelCompleteTitle').textContent='Level 2 Complete!'; document.getElementById('levelCompleteMsg').innerHTML='Great job!<br>Click below to go to Level 3.'; document.getElementById('nextLevelBtn').style.display='inline-block'; }
      if(currentLevel===3){ document.getElementById('levelCompleteTitle').textContent='Level 3 Complete!'; document.getElementById('levelCompleteMsg').innerHTML='You finished all levels! Refresh to play again.'; document.getElementById('nextLevelBtn').style.display='none'; }
    }
  </script>
</body>
</html>
