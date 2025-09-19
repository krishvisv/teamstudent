---
layout: base
title: LxD Game
permalink: /LxDgame
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
      background: #fff;
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
    .correct {
      color: #2e8b57;
      font-weight: bold;
    }
    .incorrect {
      color: #c0392b;
      font-weight: bold;
    }
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
      color: #fff;
      transform: scale(1.06);
    }
    @keyframes fadeInNext {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .level-btn {
      position: fixed;
      right: 1rem;
      background: #e3b1d9ff;
      color: #571d2aff;
      border: none;
      padding: 0.6rem 0.9rem;
      border-radius: 6px;
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0,0,0,0.12);
      font-size: 1rem;
      margin-bottom: 0.7rem;
      z-index: 10;
      transition: background 0.2s, color 0.2s, transform 0.12s;
    }
    .level-btn.level2 {
      top: 6rem;
    }
    .level-btn.level3 {
      top: 8.5rem;
    }
    .level-btn.active, .level-btn.level3.active {
      background: #e3b1d9ff;
      color: #571d2aff;
      font-weight: 700;
      transform: scale(1.06);
    }
    /* Level 3 explanation panel */
    #explanationPanel {
      display:none;
      position:fixed;
      top:5rem;
      right:1rem;
      width:300px;
      max-width:90vw;
      background:#fff;
      border-radius:10px;
      box-shadow:0 2px 12px rgba(0,0,0,0.15);
      padding:1rem;
      font-size:0.95rem;
      line-height:1.4;
      z-index: 9;
    }
    #explanationPanel h3 {
      margin-top:0;
      font-size:1.1rem;
      color:#4c4065ff;
    }
  </style>
</head>
<body>
  <button id="level2Btn" class="level-btn level2">Level Two</button>
  <button id="level3Btn" class="level-btn level3">Level Three</button>
  
  <div class="game-container start-aesthetic" id="startScreen" style="display:flex; flex-direction:column; align-items:flex-start; gap:1.2rem; background: #515170ff;">
    <h1 style="font-size:2.1rem; font-weight:900; color:#181828; margin-bottom:0.2rem; letter-spacing:1px; text-shadow:0 2px 12px rgba(76,64,101,0.10);">Welcome to Code Identify!</h1>
    <ul style="list-style:none; padding:0; margin:0 0 1.2rem 0; color:#232336;">
      <li style="margin-bottom:0.7rem; font-size:1.13rem; font-weight:500;">• Test your skills by matching code snippets to their language.</li>
      <li style="margin-bottom:0.7rem; font-size:1.13rem; font-weight:500;">• Each round, a code snippet appears.</li>
      <li style="margin-bottom:0.7rem; font-size:1.13rem; font-weight:500;">• Choose the correct language from the options.</li>
      <li style="margin-bottom:0.7rem; font-size:1.13rem; font-weight:500;">• Try to get as many correct as you can!</li>
    </ul>
    <button class="option-btn start-btn-aesthetic" id="startBtn" style="font-size:1.18rem; padding:0.95rem 2.5rem; font-weight:700; background: #978ec8ff; color:#fff; border:none; border-radius:10px; box-shadow:0 2px 12px rgba(76,64,101,0.10); transition:background 0.2s,transform 0.15s; align-self:center;">Start Game</button>
  </div>

  <div class="game-container" id="gameContainer" style="display:none;">
    <div id="progressBarContainer" style="width:100%; margin-bottom:1.2rem;">
      <div style="font-size:1.05rem; color:#4c4065ff; font-weight:600; margin-bottom:0.3rem;">Progress: <span id="progressText">0 / 15</span></div>
      <div style="background:#e3e3f7; border-radius:8px; width:100%; height:18px; overflow:hidden;">
        <div id="progressBar" style="background:linear-gradient(90deg,#9797d4 60%,#4c4065 100%); height:100%; width:0%; border-radius:8px; transition:width 0.3s;"></div>
      </div>
    </div>
    <h2 style="color:#4c4065ff;">Code Identify Game</h2>
    <div class="code-block" id="codeBlock">Loading...</div>
    <div class="options-bar" id="optionsBar"></div>
    <div class="result-message" id="resultMessage"></div>
    <button class="next-btn" id="nextBtn">Next</button>
  </div>

  <div class="game-container start-aesthetic" id="levelCompleteScreen" style="display:none; flex-direction:column; align-items:center; justify-content:center; min-height:220px; background: #515170ff !important;">
    <h2 id="levelCompleteTitle" style="color: #181828; margin-bottom:1.2rem;">Level Complete!</h2>
    <p id="levelCompleteMsg" style="font-size:1.15rem; color:#232336; margin-bottom:1.5rem;">You answered 15 questions correctly!<br>Click below to go to the next level.</p>
    <button class="option-btn" id="nextLevelBtn" style="font-size:1.1rem; padding:0.8rem 2.2rem;">Go to Next Level</button>
  </div>

  <div id="game-container">
    <div id="stats-container"></div>
    <div class="game-container" id="gameContainer" style="display:none;">
      <div id="progressBarContainer" style="width:100%; margin-bottom:1.2rem;">
        <div style="font-size:1.05rem; color:#4c4065ff; font-weight:600; margin-bottom:0.3rem;">Progress: <span id="progressText">0 / 15</span></div>
        <div style="background:#e3e3f7; border-radius:8px; width:100%; height:18px; overflow:hidden;">
          <div id="progressBar" style="background:linear-gradient(90deg,#9797d4 60%,#4c4065 100%); height:100%; width:0%; border-radius:8px; transition:width 0.3s;"></div>
        </div>
      </div>
      <h2 style="color:#4c4065ff;">Code Identify Game</h2>
      <div class="code-block" id="codeBlock">Loading...</div>
      <div class="options-bar" id="optionsBar"></div>
      <div class="result-message" id="resultMessage"></div>
      <button class="next-btn" id="nextBtn">Next</button>
    </div>
  </div>

  <div class="game-container start-aesthetic" id="levelCompleteScreen" style="display:none; flex-direction:column; align-items:center; justify-content:center; min-height:220px; background: #515170ff !important;">
    <h2 id="levelCompleteTitle" style="color: #181828; margin-bottom:1.2rem;">Level Complete!</h2>
    <p id="levelCompleteMsg" style="font-size:1.15rem; color:#232336; margin-bottom:1.5rem;">You answered 15 questions correctly!<br>Click below to go to the next level.</p>
    <button class="option-btn" id="nextLevelBtn" style="font-size:1.1rem; padding:0.8rem 2.2rem;">Go to Next Level</button>
  </div>

  <script>
    const codeSnippets = [
      { code: `body {\n  background: #222;\n  color: #fff;\n}`, lang: 'CSS' },
      { code: "function greet(name) {\n  return 'Hello, ' + name + '!';\n}", lang: 'Javascript' },
      { code: `def add(a, b):\n    return a + b`, lang: 'Python' },
      { code: `# Welcome to Markdown\n\n- List item 1\n- List item 2`, lang: 'Markdown' },
      { code: `<h1>Hello, world!</h1>\n<p>This is HTML.</p>`, lang: 'HTML' }
      // ... keep your other snippets as is
    ];

    const languages = ['CSS', 'Javascript', 'Python', 'Markdown', 'HTML'];
    let currentSnippet = null;
    const levelThreeSnippets = [
      {
        code: "fetch('/api/data').then(res => res.json()).then(d => console.log(d));",
        lang: 'Javascript',
        explanationCorrect: "Uses Fetch API and .then chaining — JavaScript web-request pattern.",
        explanationWrong: "Not Python/HTML/CSS/Markdown: uses JS promises and fetch()."
      },
      // ... keep your other Level 3 snippets
    ];

    const levelOneSnippets = [
      { code: "<p>Hello</p>", lang: 'HTML', explanationCorrect: "Simple HTML paragraph tag <p>.", explanationWrong: "Not JS/CSS/Python/Markdown." },
      { code: "print('Hello')", lang: 'Python', explanationCorrect: "print() outputs text in Python.", explanationWrong: "Not JS/HTML/CSS/Markdown." },
      { code: "console.log('Hi')", lang: 'Javascript', explanationCorrect: "console.log prints to console in JS.", explanationWrong: "Not Python/HTML/CSS/Markdown." },
      { code: "body { color: red; }", lang: 'CSS', explanationCorrect: "CSS property declarations inside a selector.", explanationWrong: "Not HTML/JS/Python/Markdown." },
      { code: "**bold**", lang: 'Markdown', explanationCorrect: "Double asterisks denote bold text.", explanationWrong: "Not HTML/CSS/JS/Python." }
    ];

    // mode-aware random snippet selector: prefers levelThree if enabled
    function getRandomSnippet() {
      if (levelThreeMode) return levelThreeSnippets[Math.floor(Math.random()*levelThreeSnippets.length)];
      if (currentLevel===1) return levelOneSnippets[Math.floor(Math.random()*levelOneSnippets.length)];
      return codeSnippets[Math.floor(Math.random()*codeSnippets.length)];
    }

    function showSnippet() {
      currentSnippet = getRandomSnippet();
      document.getElementById('codeBlock').textContent = currentSnippet.code;
      document.getElementById('resultMessage').textContent = '';
      document.getElementById('nextBtn').classList.remove('show');
      renderOptions();
    }
    function renderOptions() {
      const optionsBar = document.getElementById('optionsBar');
      optionsBar.innerHTML='';
      languages.forEach(lang=>{
        const btn = document.createElement('button');
        btn.className='option-btn';
        btn.textContent=lang;
        btn.onclick = ()=> checkAnswer(lang);
        optionsBar.appendChild(btn);
      });
    }


    // Progress tracking
    let correctCount = 0;
    let currentLevel = 1; // 1, 2, 3

    function updateProgressBar() {
      const pct = Math.min(100, Math.round((correctCount/15)*100));
      document.getElementById('progressBar').style.width = pct + '%';
      document.getElementById('progressText').textContent = `${correctCount} / 15`;
    }

    function resetProgress() {
      correctCount = 0;
      updateProgressBar();
    }

    function checkAnswer(selected) {
      const result = document.getElementById('resultMessage');
      const correctLanguage = currentSnippet.lang;
      // fetch explanations if present (level 3 entries include them)
      const explanationCorrect = currentSnippet && currentSnippet.explanationCorrect ? currentSnippet.explanationCorrect : '';
      const explanationWrong = currentSnippet && currentSnippet.explanationWrong ? currentSnippet.explanationWrong : '';
      if (selected === correctLanguage) {
        // Show why the correct answer is right
        result.innerHTML = '<span class="correct">Correct!</span>' + (explanationCorrect ? '<br><small style="color:#2e8b57; display:block; margin-top:6px;">Why: ' + explanationCorrect + '</small>' : '');
        result.className = 'result-message';
        document.getElementById('nextBtn').classList.add('show');
        correctCount++;
        updateProgressBar();
        languageStats[correctLanguage].correct++;
        if (correctCount >= 15) {
          setTimeout(showLevelComplete, 500);
        }
      } else {
        // Show why the chosen wrong answer is incorrect and what the correct answer is
        let wrongExplanation = explanationWrong ? explanationWrong : '';
        let correctExplanationSnippet = explanationCorrect ? explanationCorrect : '';
        let html = '<span class="incorrect">Try again!</span>';
        if (wrongExplanation) html += '<br><small style="color:#c0392b; display:block; margin-top:6px;">Why that is incorrect: ' + wrongExplanation + '</small>';
        html += '<br><small style="color:#2e8b57; display:block; margin-top:6px;">Answer: ' + correctLanguage + (correctExplanationSnippet ? ' — ' + correctExplanationSnippet : '') + '</small>';
        result.innerHTML = html;
        result.className = 'result-message';
        languageStats[selected].incorrect++;
      }
      updateStatsDisplay();
    }

    function showLevelComplete() {
      document.getElementById('gameContainer').style.display = 'none';
      document.getElementById('levelCompleteScreen').style.display = 'flex';
      let title = 'Level Complete!';
      let msg = '';
      let btn = document.getElementById('nextLevelBtn');
      if (currentLevel === 1) {
        title = 'Level 1 Complete!';
        msg = 'You answered 15 questions correctly!<br>Click below to go to Level 2.';
        btn.textContent = 'Go to Level 2';
      } else if (currentLevel === 2) {
        title = 'Level 2 Complete!';
        msg = 'Great job!<br>Click below to go to Level 3.';
        btn.textContent = 'Go to Level 3';
      } else {
        title = 'Level 3 Complete!';
        msg = 'You finished all levels!<br>Refresh to play again.';
        btn.style.display = 'none';
      }
      document.getElementById('levelCompleteTitle').textContent = title;
      document.getElementById('levelCompleteMsg').innerHTML = msg;
    }

    document.getElementById('nextBtn').onclick = showSnippet;
  // advancedMode: when true remove explicit language-word hints from displayed snippets
  let advancedMode = false;
  let levelThreeMode = false;
  const level2Btn = document.getElementById('level2Btn');
  const level3Btn = document.getElementById('level3Btn');

    function sanitizeForAdvanced(code) {
      // remove occurrences of explicit language names to make identification harder
      return code.replace(/\b(JavaScript|Javascript|Python|HTML|CSS|Markdown)\b/gi, '').trim();
    }

    function showSnippetAdvanced() {
      currentSnippet = getRandomSnippet();
      let displayCode = currentSnippet.code;
      if (advancedMode || levelThreeMode) displayCode = sanitizeForAdvanced(displayCode);
      document.getElementById('codeBlock').textContent = displayCode;
      document.getElementById('resultMessage').textContent='';
      document.getElementById('nextBtn').classList.remove('show');
      renderOptions();
    }

    function showSnippet() {
      // keep backward compatible: prefer advanced-aware function
      showSnippetAdvanced();
    }

    level2Btn.addEventListener('click', () => {
      // toggle Level Two advanced mode; if Level Three is active, ignore Level Two toggles
      if (levelThreeMode) {
        // if level three is active, toggle it off and enable Level Two
        levelThreeMode = false;
        level3Btn.classList.remove('active');
        level3Btn.textContent = 'Level Three';
      }
      advancedMode = !advancedMode;
      level2Btn.classList.toggle('active', advancedMode);
      level2Btn.textContent = advancedMode ? 'Level Two (on)' : 'Level Two';
      // immediately show a fresh snippet in the selected mode
      showSnippet();
    });

    level3Btn.addEventListener('click', () => {
      // Level Three takes precedence: it switches to a harder snippet pool
      levelThreeMode = !levelThreeMode;
      if (levelThreeMode) {
        // enable advanced sanitization for Level Three
        advancedMode = true;
        level2Btn.classList.remove('active');
        level2Btn.textContent = 'Level Two';
      }
      level3Btn.classList.toggle('active', levelThreeMode);
      level3Btn.textContent = levelThreeMode ? 'Level Three (on)' : 'Level Three';
      showSnippet();
    });

    // Only show the start screen on load
    window.onload = function() {
      document.getElementById('startScreen').style.display = 'flex';
      document.getElementById('gameContainer').style.display = 'none';
      document.getElementById('levelCompleteScreen').style.display = 'none';
      currentLevel = 1;
      resetProgress();
      updateStatsDisplay(); // Ensure stats are rendered at least once
    };

    // Start button logic: hide start, show game, start game
    document.getElementById('startBtn').onclick = function() {
      document.getElementById('startScreen').style.display = 'none';
      document.getElementById('gameContainer').style.display = 'block';
      document.getElementById('levelCompleteScreen').style.display = 'none';
      currentLevel = 1;
      resetProgress();
      updateStatsDisplay(); // Ensure stats are rendered when game starts
      showSnippet();
    };

    // Next level button logic
    document.getElementById('nextLevelBtn').onclick = function() {
      document.getElementById('levelCompleteScreen').style.display = 'none';
      document.getElementById('gameContainer').style.display = 'block';
      resetProgress();
      currentLevel++;
      // Set mode for next level
      if (currentLevel === 2) {
        advancedMode = true;
        level2Btn.classList.add('active');
        level2Btn.textContent = 'Level Two (on)';
        levelThreeMode = false;
        level3Btn.classList.remove('active');
        level3Btn.textContent = 'Level Three';
      } else if (currentLevel === 3) {
        levelThreeMode = true;
        level3Btn.classList.add('active');
        level3Btn.textContent = 'Level Three (on)';
        advancedMode = true;
        level2Btn.classList.remove('active');
        level2Btn.textContent = 'Level Two';
      }
      showSnippet();
    };

    let currentQuestion = 0;
    let score = 0;

    // Track correct/incorrect counts per language
    const languageStats = {};
    languages.forEach(lang => {
      languageStats[lang] = { correct: 0, incorrect: 0 };
    });

    function updateStatsDisplay() {
      let statsHtml = '<div id="language-stats" style="margin-bottom:1em;">';
      statsHtml += '<h3>Language Stats</h3>';
      statsHtml += '<table style="width:100%;text-align:center;border-collapse:collapse;">';
      statsHtml += '<tr><th>Language</th><th>Correct</th><th>Incorrect</th></tr>';
      languages.forEach(lang => {
        statsHtml += `<tr><td>${lang}</td><td>${languageStats[lang].correct}</td><td>${languageStats[lang].incorrect}</td></tr>`;
      });
      statsHtml += '</table></div>';
      document.getElementById('stats-container').innerHTML = statsHtml;
    }

    function showQuestion() {
        updateStatsDisplay();
        currentSnippet = getRandomSnippet();
        document.getElementById('codeBlock').textContent = currentSnippet.code;
        document.getElementById('resultMessage').textContent = '';
        document.getElementById('nextBtn').classList.remove('show');
        renderOptions();
    }

    // (removed duplicate checkAnswer)
  </script>
</body>
</html>
