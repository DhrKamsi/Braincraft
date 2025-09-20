<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BrainCraft Quiz App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      color: #333;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      max-width: 600px;
      width: 100%;
    }
    h1 {
      text-align: center;
      color: #6a0dad;
    }
    .question {
      font-size: 18px;
      margin-bottom: 15px;
    }
    .options button {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 10px;
      background: #eee;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }
    .options button:hover {
      background: #d1c4e9;
    }
    #next-btn {
      margin-top: 15px;
      padding: 10px 15px;
      background: #6a0dad;
      color: #fff;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      display: none;
    }
    #result {
      text-align: center;
      font-size: 20px;
      margin-top: 15px;
      display: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>BrainCraft Quiz</h1>
    <div id="quiz-box">
      <div id="question" class="question">Loading question...</div>
      <div id="options" class="options"></div>
      <button id="next-btn">Next</button>
    </div>
    <div id="result"></div>
  </div>  <script>
    const questions = [
      {
        question: "What is the capital of France?",
        options: ["Berlin", "Paris", "Rome", "Madrid"],
        answer: 1
      },
      {
        question: "Which planet is known as the Red Planet?",
        options: ["Earth", "Venus", "Mars", "Jupiter"],
        answer: 2
      },
      {
        question: "Who wrote 'Hamlet'?",
        options: ["William Wordsworth", "Charles Dickens", "William Shakespeare", "Jane Austen"],
        answer: 2
      }
    ];

    let currentQuestion = 0;
    let score = 0;

    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const nextBtn = document.getElementById("next-btn");
    const resultEl = document.getElementById("result");

    function loadQuestion() {
      const q = questions[currentQuestion];
      questionEl.textContent = q.question;
      optionsEl.innerHTML = "";
      q.options.forEach((opt, i) => {
        const btn = document.createElement("button");
        btn.textContent = opt;
        btn.onclick = () => checkAnswer(i);
        optionsEl.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      if (selected === questions[currentQuestion].answer) {
        score++;
      }
      Array.from(optionsEl.children).forEach((btn, i) => {
        btn.disabled = true;
        if (i === questions[currentQuestion].answer) {
          btn.style.background = "#a5d6a7";
        } else if (i === selected) {
          btn.style.background = "#ef9a9a";
        }
      });
      nextBtn.style.display = "block";
    }

    nextBtn.onclick = () => {
      currentQuestion++;
      if (currentQuestion < questions.length) {
        loadQuestion();
        nextBtn.style.display = "none";
      } else {
        showResult();
      }
    };

    function showResult() {
      document.getElementById("quiz-box").style.display = "none";
      resultEl.style.display = "block";
      resultEl.textContent = `You scored ${score} out of ${questions.length}!`;
    }

    loadQuestion();
  </script></body>
</html>
