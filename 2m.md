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