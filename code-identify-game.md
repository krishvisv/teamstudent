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
      background: #0078d7;
      color: #fff;
      border: none;
      border-radius: 6px;
      padding: 0.7rem 1.5rem;
      font-size: 1rem;
      cursor: pointer;
      transition: background 0.2s;
    }
    .option-btn:hover {
      background: #005fa3;
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
      background: #28a745;
      color: #fff;
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
  </style>
</head>
<body>
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

    function getRandomSnippet() {
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
    window.onload = showSnippet;
  </script>
</body>
</html>
