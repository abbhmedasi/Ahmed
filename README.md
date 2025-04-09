<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tic Tac Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f0f0f0;
    }
    h1 {
      margin-top: 20px;
    }
    #game {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 10px;
      justify-content: center;
      margin: 20px auto;
    }
    .cell {
      width: 100px;
      height: 100px;
      background-color: white;
      font-size: 2em;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      border: 2px solid #333;
    }
    #status {
      font-size: 1.2em;
      margin-top: 10px;
    }
    #restart {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 1em;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <div id="game">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>
  <p id="status">Current Player: X</p>
  <button id="restart">Restart Game</button>

  <script>
    const cells = document.querySelectorAll('.cell');
    const statusText = document.getElementById('status');
    const restartBtn = document.getElementById('restart');

    let currentPlayer = 'X';
    let gameBoard = Array(9).fill('');
    let isGameActive = true;

    const winningCombos = [
      [0,1,2],[3,4,5],[6,7,8],
      [0,3,6],[1,4,7],[2,5,8],
      [0,4,8],[2,4,6]
    ];

    function checkWinner() {
      for (let combo of winningCombos) {
        const [a, b, c] = combo;
        if (gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c]) {
          statusText.textContent = `${gameBoard[a]} wins!`;
          isGameActive = false;
          return;
        }
      }

      if (!gameBoard.includes('')) {
        statusText.textContent = "It's a draw!";
        isGameActive = false;
      }
    }

    function handleClick(e) {
      const index = e.target.dataset.index;
      if (gameBoard[index] || !isGameActive) return;

      gameBoard[index] = currentPlayer;
      e.target.textContent = currentPlayer;
      checkWinner();

      if (isGameActive) {
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        statusText.textContent = `Current Player: ${currentPlayer}`;
      }
    }

    function restartGame() {
      gameBoard.fill('');
      isGameActive = true;
      currentPlayer = 'X';
      statusText.textContent = `Current Player: ${currentPlayer}`;
      cells.forEach(cell => cell.textContent = '');
    }

    cells.forEach(cell => cell.addEventListener('click', handleClick));
    restartBtn.addEventListener('click', restartGame);
  </script>
</body>
</html>

