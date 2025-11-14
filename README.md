<!DOCTYPE html><html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>لعبة المتاهة</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background: #111;
      color: white;
      font-family: sans-serif;
    }
    canvas {
      border: 3px solid white;
      background: #222;
    }
  </style>
</head>
<body>
  <canvas id="maze" width="400" height="400"></canvas>  <script>
    const canvas = document.getElementById("maze");
    const ctx = canvas.getContext("2d");

    const tile = 40;
    const maze = [
      [1,1,1,1,1,1,1,1,1,1],
      [1,0,0,0,1,0,0,0,0,1],
      [1,0,1,0,1,0,1,1,0,1],
      [1,0,1,0,0,0,0,1,0,1],
      [1,0,1,1,1,1,0,1,0,1],
      [1,0,0,0,0,1,0,1,0,1],
      [1,1,1,1,0,1,0,1,0,1],
      [1,0,0,1,0,0,0,0,0,1],
      [1,0,1,0,0,1,1,1,0,1],
      [1,1,1,1,1,1,1,1,1,1]
    ];

    let player = { x: 1, y: 1 };
    const goal = { x: 8, y: 8 };

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      for (let y = 0; y < 10; y++) {
        for (let x = 0; x < 10; x++) {
          if (maze[y][x] === 1) {
            ctx.fillStyle = "#555";
            ctx.fillRect(x * tile, y * tile, tile, tile);
          }
        }
      }

      // رسم كعكة عيد ميلاد
      const gx = goal.x * tile;
      const gy = goal.y * tile;
      const midX = gx + tile / 2;

      // قاعدة الكعكة
      ctx.fillStyle = "#d35400";
      ctx.fillRect(gx + 5, gy + 15, 30, 15);

      // طبقة الكريمة
      ctx.fillStyle = "#f1c40f";
      ctx.fillRect(gx + 5, gy + 10, 30, 7);

      // الشمعة
      ctx.fillStyle = "#ffffff";
      ctx.fillRect(midX - 2, gy + 2, 4, 10);

      // لهب الشمعة
      ctx.beginPath();
      ctx.arc(midX, gy + 2, 3, 0, Math.PI * 2);
      ctx.fillStyle = "#ffcc00";
      ctx.fill();

      // رسم اللاعب كفتاة بسيطة (رأس، شعر، عينين، فستان)
      const px = player.x * tile;
      const py = player.y * tile;
      const centerX = px + tile/2;
      const centerY = py + tile/2 - 4;

      // فستان (مثلث)
      ctx.beginPath();
      ctx.moveTo(centerX - 10, centerY + 12);
      ctx.lineTo(centerX + 10, centerY + 12);
      ctx.lineTo(centerX, centerY + 28);
      ctx.closePath();
      ctx.fillStyle = "#e74c3c"; // لون الفستان
      ctx.fill();

      // رأس
      ctx.beginPath();
      ctx.arc(centerX, centerY - 8, 10, 0, Math.PI * 2);
      ctx.fillStyle = "#f1c27d"; // لون البشرة
      ctx.fill();

      // شعر
      ctx.beginPath();
      ctx.arc(centerX, centerY - 10, 11, Math.PI, 2 * Math.PI);
      ctx.fillStyle = "#2c2c2c"; // لون الشعر
      ctx.fill();

      // عيون
      ctx.fillStyle = "#000";
      ctx.beginPath();
      ctx.arc(centerX - 4, centerY - 10, 1.6, 0, Math.PI * 2);
      ctx.fill();
      ctx.beginPath();
      ctx.arc(centerX + 4, centerY - 10, 1.6, 0, Math.PI * 2);
      ctx.fill();

      // لمعة بسيطة في العين اليمنى
      ctx.fillStyle = "rgba(255,255,255,0.8)";
      ctx.beginPath();
      ctx.arc(centerX + 5, centerY - 11, 0.8, 0, Math.PI * 2);
      ctx.fill();

      // حواف خفيفة
      ctx.strokeStyle = "rgba(0,0,0,0.2)";
      ctx.lineWidth = 0.8;
      ctx.stroke();
    }
function move(dx, dy) {
      const nx = player.x + dx;
      const ny = player.y + dy;

      if (maze[ny][nx] === 0) {
        player.x = nx;
        player.y = ny;
      }

      if (player.x === goal.x && player.y === goal.y) {
        const input = prompt("أحسنتِ صنعًا ! تبقت خطوة واحدة للانتصار ، أدخلي تاريخ ميلادك (استعملي / كفواصل)");
        if (input !== "14/11/2008") {
          alert("يرجى المحاولة مجددًا");
        } else {
          alert("أحسنتِ صنعًا ! الآن عودي إلى الدردشة و أرسلي كلمة \"باركلي\"");
        }
      }

      draw();
    }

    document.addEventListener("keydown", (e) => {
      if (e.key === "ArrowUp") move(0, -1);
      if (e.key === "ArrowDown") move(0, 1);
      if (e.key === "ArrowLeft") move(-1, 0);
      if (e.key === "ArrowRight") move(1, 0);
    });

    draw();
  </script>  <div style="position: fixed; bottom: 20px; display: flex; flex-direction: column; gap: 10px; left: 50%; transform: translateX(-50%);">
    <button style="padding: 10px 20px; font-size: 18px;" onclick="move(0, -1)">⬆️</button>
    <div style="display: flex; gap: 10px; justify-content: center;">
      <button style="padding: 10px 20px; font-size: 18px;" onclick="move(-1, 0)">⬅️</button>
      <button style="padding: 10px 20px; font-size: 18px;" onclick="move(1, 0)">➡️</button>
    </div>
    <button style="padding: 10px 20px; font-size: 18px;" onclick="move(0, 1)">⬇️</button>
  </div></body>
</html>
