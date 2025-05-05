# Tictactoe-
Fun game 1v1 
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe - 2 Pemain</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #74ebd5, #ACB6E5);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }h1 {
  color: #333;
  margin-bottom: 20px;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 10px;
}

.cell {
  width: 100px;
  height: 100px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
  font-size: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.3s ease, background 0.3s ease;
}

.cell:hover {
  transform: scale(1.05);
  background: #f0f0f0;
}

.status {
  margin-top: 20px;
  font-size: 1.2rem;
  color: #333;
}

button {
  margin-top: 15px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

  </style>
</head>
<body>
  <h1>Tic Tac Toe - 2 Pemain</h1>
  <div class="board" id="board"></div>
  <div class="status" id="status">Giliran Pemain: X</div>
  <button onclick="resetGame()">Reset Game</button>  <script>
    const board = document.getElementById("board");
    const status = document.getElementById("status");
    let cells = [];
    let currentPlayer = "X";
    let gameOver = false;

    function createBoard() {
      board.innerHTML = "";
      cells = [];
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.addEventListener("click", () => handleMove(cell, i));
        board.appendChild(cell);
        cells.push("");
      }
    }

    function handleMove(cell, index) {
      if (gameOver || cells[index]) return;

      cell.textContent = currentPlayer;
      cells[index] = currentPlayer;

      if (checkWinner()) {
        status.textContent = `Pemain ${currentPlayer} Menang!`;
        gameOver = true;
      } else if (!cells.includes("")) {
        status.textContent = "Seri!";
        gameOver = true;
      } else {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
        status.textContent = `Giliran Pemain: ${currentPlayer}`;
      }
    }

    function checkWinner() {
      const wins = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];

      return wins.some(comb => {
        const [a, b, c] = comb;
        return cells[a] && cells[a] === cells[b] && cells[a] === cells[c];
      });
    }

    function resetGame() {
      currentPlayer = "X";
      gameOver = false;
      status.textContent = `Giliran Pemain: ${currentPlayer}`;
      createBoard();
    }

    createBoard();
  </script></body>
</html>