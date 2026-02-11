# Valentine
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Harsh, Will You Be My Valentine?</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      height: 100vh;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #ff758c, #ff7eb3);
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      text-align: center;
      overflow: hidden;
    }

    .card {
      background: rgba(255, 255, 255, 0.15);
      padding: 40px 30px;
      border-radius: 20px;
      backdrop-filter: blur(10px);
      max-width: 400px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
      z-index: 2;
      position: relative;
    }

    h1 {
      font-size: 2.2rem;
      margin-bottom: 10px;
    }

    p {
      font-size: 1.1rem;
      margin-bottom: 30px;
    }

    button {
      font-size: 1rem;
      padding: 12px 25px;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      margin: 10px;
      transition: transform 0.2s;
      position: relative;
    }

    .yes {
      background: #fff;
      color: #ff4d6d;
      font-weight: bold;
    }

    .no {
      background: transparent;
      color: white;
      border: 2px solid white;
    }

    #message {
      margin-top: 20px;
      font-size: 1.2rem;
      display: none;
    }

    /* Floating hearts */
    .heart {
      position: absolute;
      bottom: -20px;
      color: rgba(255, 255, 255, 0.8);
      font-size: 20px;
      animation: floatUp linear forwards;
      pointer-events: none;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0);
        opacity: 1;
      }
      to {
        transform: translateY(-110vh);
        opacity: 0;
      }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 5;
    }
  </style>
</head>
<body>

<canvas id="confetti"></canvas>

<div class="card">
  <h1>Harsh ❤️</h1>
  <p>
    I have something special to ask you…<br>
    Will you be my Valentine? 💌
  </p>

  <button class="yes" onclick="yesClicked()">Yes 💕</button>
  <button class="no" id="noBtn">No 🙈</button>

  <div id="message"></div>
</div>

<script>
  /* NO button escape */
  const noBtn = document.getElementById("noBtn");
  noBtn.addEventListener("mouseenter", () => {
    const x = Math.random() * 200 - 100;
    const y = Math.random() * 200 - 100;
    noBtn.style.transform = `translate(${x}px, ${y}px)`;
  });

  /* Floating hearts generator */
  function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = Math.random() * 20 + 15 + "px";
    heart.style.animationDuration = Math.random() * 3 + 4 + "s";

    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 7000);
  }

  setInterval(createHeart, 500);

  /* CONFETTI */
  const canvas = document.getElementById("confetti");
  const ctx = canvas.getContext("2d");
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  let confettiPieces = [];

  function launchConfetti() {
    confettiPieces = [];
    for (let i = 0; i < 200; i++) {
      confettiPieces.push({
        x: canvas.width / 2,
        y: canvas.height / 2,
        vx: (Math.random() - 0.5) * 10,
        vy: (Math.random() - 0.5) * 10,
        size: Math.random() * 6 + 4,
        color: `hsl(${Math.random() * 360}, 100%, 70%)`,
      });
    }
    animateConfetti();
  }

  function animateConfetti() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    confettiPieces.forEach(p => {
      p.x += p.vx;
      p.y += p.vy;
      p.vy += 0.05;
      ctx.fillStyle = p.color;
      ctx.fillRect(p.x, p.y, p.size, p.size);
    });
    requestAnimationFrame(animateConfetti);
  }

  function yesClicked() {
    const msg = document.getElementById("message");
    msg.style.display = "block";
    msg.innerHTML = "YAYYY!! 💖 Harsh, you’re officially my Valentine 🥰";
    launchConfetti();
  }
</script>

</body>
</html>
