git remoto adicionar origem https://github.com/Coelho7kook/Deszeldas.git
 git branch -M main 
git push -u origin main


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Zelda-like Game</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #000;
      margin: 0;
      font-family: Arial, sans-serif;
    }

    #game {
      width: 400px;
      height: 300px;
      border: 2px solid #333;
      background-color: #7f7f7f;
      position: relative;
    }

    #player {
      width: 32px;
      height: 32px;
      background-color: #00f;
      position: absolute;
      bottom: 0;
      left: 0;
    }

    #item {
      width: 16px;
      height: 16px;
      background-color: #ff0;
      position: absolute;
      bottom: 80px;
      left: 180px;
    }
  </style>
</head>
<body>
  <div id="game">
    <div id="player"></div>
    <div id="item"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>




document.addEventListener('DOMContentLoaded', function() {
  const player = document.getElementById('player');
  const item = document.getElementById('item');
  const game = document.getElementById('game');

  let playerX = 0;
  const playerSpeed = 4;

  function updatePlayerPosition() {
    player.style.left = `${playerX}px`;
  }

  function movePlayer(direction) {
    if (direction === 'left') {
      playerX -= playerSpeed;
      if (playerX < 0) {
        playerX = 0;
      }
    } else if (direction === 'right') {
      playerX += playerSpeed;
      const gameWidth = game.offsetWidth;
      if (playerX + player.offsetWidth > gameWidth) {
        playerX = gameWidth - player.offsetWidth;
      }
    }

    updatePlayerPosition();
  }

  document.addEventListener('keydown', function(event) {
    if (event.key === 'ArrowLeft') {
      movePlayer('left');
    } else if (event.key === 'ArrowRight') {
      movePlayer('right');
    }
  });

  // Detecção de colisão simples
  function checkCollision() {
    const playerRect = player.getBoundingClientRect();
    const itemRect = item.getBoundingClientRect();

    if (
      playerRect.left < itemRect.right &&
      playerRect.right > itemRect.left &&
      playerRect.top < itemRect.bottom &&
      playerRect.bottom > itemRect.top
    ) {
      alert('Você encontrou o item!');
      item.style.display = 'none'; // Esconde o item após coletar
    }
  }

  // Verifica colisão a cada intervalo
  setInterval(checkCollision, 100);
});
