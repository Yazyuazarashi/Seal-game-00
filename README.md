# Seal-game-00
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Sealvivors</title>
  <style>
    html, body {
      margin: 0;
      overflow: hidden;
      background: #d0f0ff;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <canvas id="gameCanvas" width="800" height="600"></canvas>
  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    let scale = 1;
    let offsetX = 0;
    let offsetY = 0;
    let dragging = false;
    let dragStart = { x: 0, y: 0 };

    const gridSize = 64;
    const mapCols = 50;
    const mapRows = 50;

    canvas.addEventListener('mousedown', (e) => {
      dragging = true;
      dragStart.x = e.clientX - offsetX;
      dragStart.y = e.clientY - offsetY;
    });

    canvas.addEventListener('mouseup', () => {
      dragging = false;
    });

    canvas.addEventListener('mousemove', (e) => {
      if (dragging) {
        offsetX = e.clientX - dragStart.x;
        offsetY = e.clientY - dragStart.y;
        draw();
      }
    });

    canvas.addEventListener('wheel', (e) => {
      e.preventDefault();
      const zoom = e.deltaY > 0 ? 0.9 : 1.1;
      scale *= zoom;
      draw();
    });

    function draw() {
      ctx.setTransform(scale, 0, 0, scale, offsetX, offsetY);
      ctx.clearRect(-offsetX / scale, -offsetY / scale, canvas.width / scale, canvas.height / scale);

      for (let y = 0; y < mapRows; y++) {
        for (let x = 0; x < mapCols; x++) {
          ctx.strokeStyle = "#cccccc";
          ctx.strokeRect(x * gridSize, y * gridSize, gridSize, gridSize);
        }
      }
    }

    draw();
  </script>
</body>
</html>