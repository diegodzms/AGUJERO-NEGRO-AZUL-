<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Agujero Negro de Corazones</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }body {
  overflow: hidden;
  background: radial-gradient(circle at center, #0b0b18 0%, #000000 70%);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

canvas {
  width: 100vw;
  height: 100vh;
  display: block;
}

.title {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 2rem;
  letter-spacing: 3px;
  text-shadow: 0 0 10px #ff66cc;
  z-index: 10;
}

  </style>
</head>
<body>
  <div class="title">AGUJERO NEGRO DE CORAZONES</div>
  <canvas id="scene"></canvas>  <script>
    const canvas = document.getElementById('scene');
    const ctx = canvas.getContext('2d');

    function resize() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    resize();
    window.addEventListener('resize', resize);

    const center = {
      x: () => canvas.width / 2,
      y: () => canvas.height / 2
    };

    const hearts = [];
    const totalHearts = 450;

    class Heart {
      constructor() {
        this.angle = Math.random() * Math.PI * 2;
        this.radius = 140 + Math.random() * 240;
        this.size = 6 + Math.random() * 10;
        this.speed = 0.002 + Math.random() * 0.006;
        this.color = `hsl(${330 + Math.random() * 30}, 100%, ${60 + Math.random() * 20}%)`;
        this.offset = Math.random() * 20;
      }

      drawHeart(x, y, size) {
        ctx.save();
        ctx.translate(x, y);
        ctx.scale(size / 15, size / 15);

        ctx.beginPath();
        ctx.moveTo(0, 0);
        ctx.bezierCurveTo(0, -3, -5, -8, -10, -8);
        ctx.bezierCurveTo(-20, -8, -20, 7, -20, 7);
        ctx.bezierCurveTo(-20, 15, -10, 22, 0, 28);
        ctx.bezierCurveTo(10, 22, 20, 15, 20, 7);
        ctx.bezierCurveTo(20, 7, 20, -8, 10, -8);
        ctx.bezierCurveTo(5, -8, 0, -3, 0, 0);

        ctx.fillStyle = this.color;
        ctx.shadowBlur = 20;
        ctx.shadowColor = this.color;
        ctx.fill();
        ctx.restore();
      }

      update() {
        this.angle += this.speed;

        const warpedX = Math.cos(this.angle) * this.radius;
        const warpedY = Math.sin(this.angle) * (this.radius * 0.28);

        const distortion = 1 + Math.sin(this.angle * 2 + this.offset) * 0.2;

        const x = center.x() + warpedX * distortion;
        const y = center.y() + warpedY;

        this.drawHeart(x, y, this.size);
      }
    }

    for (let i = 0; i < totalHearts; i++) {
      hearts.push(new Heart());
    }

    function drawBlackHole() {
      const x = center.x();
      const y = center.y();

      // Halo gravitacional
      const glow = ctx.createRadialGradient(x, y, 40, x, y, 180);
      glow.addColorStop(0, 'rgba(255,255,255,0.05)');
      glow.addColorStop(0.4, 'rgba(120,120,255,0.08)');
      glow.addColorStop(1, 'rgba(0,0,0,0)');

      ctx.beginPath();
      ctx.fillStyle = glow;
      ctx.arc(x, y, 180, 0, Math.PI * 2);
      ctx.fill();

      // Disco luminoso
      const disk = ctx.createRadialGradient(x, y, 70, x, y, 130);
      disk.addColorStop(0, 'rgba(255,180,220,0)');
      disk.addColorStop(0.5, 'rgba(255,120,200,0.35)');
      disk.addColorStop(1, 'rgba(255,255,255,0)');

      ctx.beginPath();
      ctx.fillStyle = disk;
      ctx.ellipse(x, y, 130, 45, 0, 0, Math.PI * 2);
      ctx.fill();

      // Agujero negro central
      ctx.beginPath();
      ctx.arc(x, y, 75, 0, Math.PI * 2);
      ctx.fillStyle = '#000';
      ctx.shadowBlur = 50;
      ctx.shadowColor = '#000';
      ctx.fill();
    }

    function stars() {
      for (let i = 0; i < 120; i++) {
        const x = Math.random() * canvas.width;
        const y = Math.random() * canvas.height;
        const r = Math.random() * 2;

        ctx.beginPath();
        ctx.arc(x, y, r, 0, Math.PI * 2);
        ctx.fillStyle = 'rgba(255,255,255,0.8)';
        ctx.fill();
      }
    }

    stars();

    function animate() {
      ctx.fillStyle = 'rgba(0,0,0,0.15)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      drawBlackHole();

      hearts.forEach(heart => heart.update());

      requestAnimationFrame(animate);
    }

    animate();
  </script></body>
</html>