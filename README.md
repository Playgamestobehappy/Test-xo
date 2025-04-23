<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>XO Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f0f0f0;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
    }
    .cell {
      background: white;
      border: 2px solid #333;
      font-size: 2em;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
    }
  </style>
</head>
<body>

<div class="board" id="board"></div>

<script>
  const board = document.getElementById('board');
  let currentPlayer = 'X';
  let cells = [];

  function checkWinner() {
    const lines = [
      [0,1,2], [3,4,5], [6,7,8], // rows
      [0,3,6], [1,4,7], [2,5,8], // columns
      [0,4,8], [2,4,6]           // diagonals
    ];

    for (let line of lines) {
      const [a, b, c] = line;
      if (cells[a].textContent &&
          cells[a].textContent === cells[b].textContent &&
          cells[a].textContent === cells[c].textContent) {
        alert(`Player ${cells[a].textContent} wins!`);
        resetBoard();
        return;
      }
    }

    if ([...cells].every(cell => cell.textContent)) {
      alert("It's a draw!");
      resetBoard();
    }
  }

  function resetBoard() {
    cells.forEach(cell => cell.textContent = '');
    currentPlayer = 'X';
  }

  function createBoard() {
    for (let i = 0; i < 9; i++) {
      const cell = document.createElement('div');
      cell.classList.add('cell');
      cell.addEventListener('click', () => {
        if (cell.textContent === '') {
          cell.textContent = currentPlayer;
          currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
          checkWinner();
        }
      });
      board.appendChild(cell);
      cells.push(cell);
    }
  }

  createBoard();
</script>

</body>
</html>
