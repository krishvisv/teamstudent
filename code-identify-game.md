---
layout: base
title: LxD Game
permalink: /LxDgame
comments: true
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Code Identify Game</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      /* pastel pink -> pastel blue gradient */
      background: linear-gradient(135deg, #ffd1dc 0%, #cfe8ff 100%);
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
      /* pastel blue buttons */
      background: #9bd0ff;
      color: #013a63;
      border: none;
      border-radius: 6px;
      padding: 0.7rem 1.5rem;
      font-size: 1rem;
      cursor: pointer;
      transition: background 0.2s, transform 0.06s;
    }
    .option-btn:hover {
      background: #74baff;
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
      /* pastel pink next */
      background: #ffb6c1;
      color: #3a1f25;
      border: none;
      border-radius: 6px;
      padding: 0.6rem 1.2rem;
      font-size: 1rem;
      cursor: pointer;
      display: none;
    }
    .next-btn.show {
      display: inline-block;
    }
    /* Level toggle button (floating on the right) */
    .level-btn {
      position: fixed;
      right: 1rem;
      top: 6rem;
      background: #ff9fb1; /* pastel pink */
      color: #3a1f25;
      border: none;
      padding: 0.6rem 0.9rem;
      border-radius: 6px;
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0,0,0,0.12);
    }
    .level-btn.active { background: #ff7f95; }
    .level-btn.level3 {
      top: 10rem;
      background: #9bd0ff; /* pastel blue for Level Three */
      color: #013a63;
    }
    .level-btn.level3.active { background: #74baff; }
  </style>
</head>
<body>
  <button id="levelBtn" class="level-btn">Level Two</button>
  <button id="level3Btn" class="level-btn level3">Level Three</button>
  <div class="game-container">
    <h2>Code Identify Game</h2>
    <div class="code-block" id="codeBlock">Loading...</div>
    <div class="options-bar" id="optionsBar"></div>
    <div class="result-message" id="resultMessage"></div>
    <button class="next-btn" id="nextBtn">Next</button>
  </div>
  <script>
    const codeSnippets = [
      {
        code: `body {\n  background: #222;\n  color: #fff;\n}`,
        lang: 'CSS'
      },
      {
        code: "function greet(name) {\n  return 'Hello, ' + name + '!';\n}",
        lang: 'Javascript'
      },
      {
        code: `def add(a, b):\n    return a + b`,
        lang: 'Python'
      },
      {
        code: `# Welcome to Markdown\n\n- List item 1\n- List item 2`,
        lang: 'Markdown'
      },
      {
        code: `<h1>Hello, world!</h1>\n<p>This is HTML.</p>`,
        lang: 'HTML'
      },
      {
        code: `console.log('JavaScript is fun!');`,
        lang: 'Javascript'
      },
      {
        code: `**Bold text** and *italic text*`,
        lang: 'Markdown'
      },
      {
        code: `for (let i = 0; i < 5; i++) {\n  console.log(i);\n}`,
        lang: 'Javascript'
      },
      {
        code: `print('Hello from Python!')`,
        lang: 'Python'
      },
      {
        code: `a {\n  color: blue;\n  text-decoration: underline;\n}`,
        lang: 'CSS'
      },
      {
        code: `<ul>\n  <li>Item 1</li>\n  <li>Item 2</li>\n</ul>`,
        lang: 'HTML'
      },
      {
        code: `<!-- This is a comment in HTML -->`,
        lang: 'HTML'
      },
      {
        code: `/* CSS comment */\n.header {\n  font-size: 2em;\n}`,
        lang: 'CSS'
      },
      {
        code: `let x = 10;\nlet y = 20;\nlet sum = x + y;`,
        lang: 'Javascript'
      },
      {
        code: `## Subheading in Markdown`,
        lang: 'Markdown'
      },
      {
        code: `if x > 0:\n    print('Positive')\nelse:\n    print('Non-positive')`,
        lang: 'Python'
      }
    ];
    const languages = ['CSS', 'Javascript', 'Python', 'Markdown', 'HTML'];
    let currentSnippet = null;

    // levelThree pool: different, harder snippets (no explicit language words)
    const levelThreeSnippets = [
      { code: "fetch('/api/data').then(res => res.json()).then(d => console.log(d));", lang: 'Javascript' },
      { code: "SELECT name, score FROM users WHERE score > 100 ORDER BY score DESC;", lang: 'Python' },
      { code: "<section><article><h2>Title</h2><p>Content here</p></article></section>", lang: 'HTML' },
      { code: "@media (min-width: 600px) { .col { display: grid; grid-template-columns: 1fr 2fr; } }", lang: 'CSS' },
      { code: "- [x] Task done\n- [ ] Task todo\n\nSome **notes** here.", lang: 'Markdown' },
      { code: "const [a,b] = arr; const result = a.map(x => x*2).filter(Boolean);", lang: 'Javascript' },
      { code: "def fib(n):\n    a,b=0,1\n    for _ in range(n):\n        a,b=b,a+b\n    return a", lang: 'Python' }
    ];

    // mode-aware random snippet selector: prefers levelThree if enabled
    function getRandomSnippet() {
      if (typeof levelThreeMode !== 'undefined' && levelThreeMode) {
        return levelThreeSnippets[Math.floor(Math.random() * levelThreeSnippets.length)];
      }
      return codeSnippets[Math.floor(Math.random() * codeSnippets.length)];
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
      optionsBar.innerHTML = '';
      languages.forEach(lang => {
        const btn = document.createElement('button');
        btn.className = 'option-btn';
        btn.textContent = lang;
        btn.onclick = () => checkAnswer(lang);
        optionsBar.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      const result = document.getElementById('resultMessage');
      if (selected === currentSnippet.lang) {
        result.textContent = 'Correct!';
        result.className = 'result-message correct';
        document.getElementById('nextBtn').classList.add('show');
      } else {
        result.textContent = 'Try again!';
        result.className = 'result-message incorrect';
      }
    }

    document.getElementById('nextBtn').onclick = showSnippet;
  // advancedMode: when true remove explicit language-word hints from displayed snippets
  let advancedMode = false;
  let levelThreeMode = false;
  const levelBtn = document.getElementById('levelBtn');
  const level3Btn = document.getElementById('level3Btn');

    function sanitizeForAdvanced(code) {
      // remove occurrences of explicit language names to make identification harder
      return code.replace(/\b(JavaScript|Javascript|Python|HTML|CSS|Markdown)\b/gi, '').trim();
    }

    function showSnippetAdvanced() {
      currentSnippet = getRandomSnippet();
      let displayCode = currentSnippet.code;
      // Level Three snippets are selected from a different pool; always sanitize if advancedMode or levelThreeMode
      if (advancedMode || levelThreeMode) displayCode = sanitizeForAdvanced(displayCode);
      document.getElementById('codeBlock').textContent = displayCode;
      document.getElementById('resultMessage').textContent = '';
      document.getElementById('nextBtn').classList.remove('show');
      renderOptions();
    }

    function showSnippet() {
      // keep backward compatible: prefer advanced-aware function
      showSnippetAdvanced();
    }

    levelBtn.addEventListener('click', () => {
      // toggle Level Two advanced mode; if Level Three is active, ignore Level Two toggles
      if (levelThreeMode) {
        // if level three is active, toggle it off and enable Level Two
        levelThreeMode = false;
        level3Btn.classList.remove('active');
        level3Btn.textContent = 'Level Three';
      }
      advancedMode = !advancedMode;
      levelBtn.classList.toggle('active', advancedMode);
      levelBtn.textContent = advancedMode ? 'Level Two (on)' : 'Level Two';
      // immediately show a fresh snippet in the selected mode
      showSnippet();
    });

    level3Btn.addEventListener('click', () => {
      // Level Three takes precedence: it switches to a harder snippet pool
      levelThreeMode = !levelThreeMode;
      if (levelThreeMode) {
        // enable advanced sanitization for Level Three
        advancedMode = true;
        levelBtn.classList.remove('active');
        levelBtn.textContent = 'Level Two';
      }
      level3Btn.classList.toggle('active', levelThreeMode);
      level3Btn.textContent = levelThreeMode ? 'Level Three (on)' : 'Level Three';
      showSnippet();
    });

    window.onload = showSnippet;
  </script>
</body>
</html>
