# Circletocircle
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Click the Circle Game</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background: #121212;
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }

    #gameArea {
      position: relative;
      width: 90vw;
      height: 70vh;
      background: #1f1f1f;
      border-radius: 20px;
      margin: 20px 0;
      overflow: hidden;
      display: none;
    }

    #circle {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: #e63946;
      position: absolute;
      cursor: pointer;
    }

    #score, #timer {
      font-size: 20px;
      margin: 5px;
    }

    .screen {
      position: absolute;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.85);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      border-radius: 20px;
      z-index: 10;
    }

    button {
      padding: 10px 20px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      background: #4caf50;
      color: white;
      cursor: pointer;
      margin-top: 15px;
    }

    button:hover {
      background: #45a049;
    }
  </style>
</head>
<body>

  <h2>Click the Circle!</h2>
  <div id="score">Score: 0</div>
  <div id="timer">Time Left: 30s</div>

  <div id="gameArea">
    <div id="circle"></div>

    <div id="startScreen" class="screen">
      <h2>Welcome!</h2>
      <button onclick="startGame()">Start Game</button>
    </div>

    <div id="endScreen" class="screen" style="display: none;">
      <h2>Time's Up!</h2>
      <p id="finalScore">Your Score: 0</p>
      <button onclick="restartGame()">Play Again</button>
    </div>
  </div>

  <script>
    const gameArea = document.getElementById("gameArea");
    const circle = document.getElementById("circle");
    const scoreDisplay = document.getElementById("score");
    const timerDisplay = document.getElementById("timer");
    const startScreen = document.getElementById("startScreen");
    const endScreen = document.getElementById("endScreen");
    const finalScore = document.getElementById("finalScore");

    let score = 0;
    let timeLeft = 30;
    let timerInterval;

    function moveCircle() {
      const maxX = gameArea.clientWidth - circle.offsetWidth;
      const maxY = gameArea.clientHeight - circle.offsetHeight;
      const randomX = Math.floor(Math.random() * maxX);
      const randomY = Math.floor(Math.random() * maxY);
      circle.style.left = randomX + "px";
      circle.style.top = randomY + "px";
    }

    function startGame() {
      score = 0;
      timeLeft = 30;
      scoreDisplay.textContent = "Score: 0";
      timerDisplay.textContent = "Time Left: 30s";
      startScreen.style.display = "none";
      endScreen.style.display = "none";
      gameArea.style.display = "block";
      circle.style.display = "block";
      moveCircle();

      timerInterval = setInterval(() => {
        timeLeft--;
        timerDisplay.textContent = "Time Left: " + timeLeft + "s";
        if (timeLeft <= 0) {
          endGame();
        }
      }, 1000);
    }

    function endGame() {
      clearInterval(timerInterval);
      circle.style.display = "none";
      finalScore.textContent = "Your Score: " + score;
      endScreen.style.display = "flex";
    }

    function restartGame() {
      startGame();
    }

    circle.addEventListener("click", () => {
      score++;
      scoreDisplay.textContent = "Score: " + score;
      moveCircle();
    });

    // Auto-show start screen
    gameArea.style.display = "block";
  </script>

</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Click the Circle</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h2>Click the Circle!</h2>
  <div id="score">Score: 0</div>
  <div id="timer">Time Left: 30s</div>

  <div id="gameArea">
    <div id="circle"></div>

    <div id="startScreen" class="screen">
      <h2>Welcome!</h2>
      <button onclick="startGame()">Start Game</button>
    </div>

    <div id="endScreen" class="screen">
      <h2>Time's Up!</h2>
      <p id="finalScore">Your Score: 0</p>
      <button onclick="restartGame()">Play Again</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
