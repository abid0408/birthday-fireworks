# birthday-fireworks<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Happy Birthday Mahi</title>
  <style>
    body {
      margin: 0;
      background-color: black;
      overflow: hidden;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: white;
      text-align: center;
    }
    h1 {
      font-size: 3em;
      margin-top: 20vh;
      animation: glow 2s ease-in-out infinite alternate;
    }
    p {
      font-size: 1.2em;
      margin-top: 20px;
    }
    @keyframes glow {
      from { text-shadow: 0 0 10px #ff4081, 0 0 20px #ff4081; }
      to { text-shadow: 0 0 20px #f06292, 0 0 30px #f06292; }
    }
    footer {
      position: absolute;
      bottom: 10px;
      width: 100%;
      font-size: 1em;
      color: #ccc;
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
    }
  </style>
</head>
<body>
  <h1>Happy Birthday Mahi!</h1>
  <p>You're the sparkle in every firework, the reason for every smile. I love you.</p>
  <footer>With all my love, Laddu</footer>

  <canvas id="fireworks"></canvas>

  <script>
    // Simple fireworks animation
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const fireworks = [];

    function createFirework() {
      const x = Math.random() * canvas.width;
      const y = Math.random() * canvas.height / 2;
      const radius = Math.random() * 3 + 2;
      const color = `hsl(${Math.random() * 360}, 100%, 70%)`;
      fireworks.push({ x, y, radius, alpha: 1, color });
    }

    function drawFireworks() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let i = 0; i < fireworks.length; i++) {
        const fw = fireworks[i];
        ctx.beginPath();
        ctx.arc(fw.x, fw.y, fw.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(${fw.color.match(/\d+/g).join(",")},${fw.alpha})`;
        ctx.fill();
        fw.alpha -= 0.01;
        fw.radius += 0.3;
        if (fw.alpha <= 0) fireworks.splice(i, 1);
      }
    }

    setInterval(() => {
      createFirework();
    }, 300);

    function animate() {
      drawFireworks();
      requestAnimationFrame(animate);
    }

    animate();

    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
