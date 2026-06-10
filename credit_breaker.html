<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>単位クラッシャー</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DotGothic16&family=Zen+Maru+Gothic:wght@700&display=swap');

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background: #0d0d1a;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  min-height: 100vh;
  font-family: 'DotGothic16', monospace;
  overflow: hidden;
  touch-action: none;
}

#header {
  width: 100%;
  max-width: 420px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 16px 6px;
  color: #fff;
}

#title {
  font-family: 'Zen Maru Gothic', sans-serif;
  font-size: 18px;
  background: linear-gradient(90deg, #ff6ee7, #7ee8ff, #ffe96e);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  letter-spacing: 1px;
}

#score-area {
  text-align: right;
  font-size: 12px;
  line-height: 1.6;
  color: #aaa;
}
#score-area span { color: #fff; font-size: 15px; }

#canvas-wrap {
  position: relative;
  width: 100%;
  max-width: 420px;
  padding: 0 8px;
}

canvas {
  display: block;
  width: 100%;
  border-radius: 12px;
  border: 1.5px solid rgba(255,255,255,0.08);
  background: #0a0a18;
  touch-action: none;
}

/* Floating notifications */
.notif {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  background: linear-gradient(135deg, #7b2fff, #ff2fb0);
  color: #fff;
  font-family: 'Zen Maru Gothic', sans-serif;
  font-size: 15px;
  padding: 8px 20px;
  border-radius: 100px;
  pointer-events: none;
  white-space: nowrap;
  z-index: 10;
  animation: popUp 1.6s ease forwards;
}
@keyframes popUp {
  0%   { opacity: 0; top: 55%; transform: translateX(-50%) scale(0.7); }
  20%  { opacity: 1; top: 50%; transform: translateX(-50%) scale(1.1); }
  60%  { opacity: 1; top: 47%; transform: translateX(-50%) scale(1); }
  100% { opacity: 0; top: 38%; transform: translateX(-50%) scale(0.9); }
}

/* Overlay screens */
#overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgba(10, 10, 24, 0.88);
  border-radius: 12px;
  gap: 14px;
  z-index: 20;
}
#overlay h2 {
  font-family: 'Zen Maru Gothic', sans-serif;
  font-size: 26px;
  background: linear-gradient(90deg, #ff6ee7, #7ee8ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
#overlay p { color: #ccc; font-size: 13px; text-align: center; line-height: 1.8; }
#overlay button {
  background: linear-gradient(135deg, #7b2fff, #ff2fb0);
  color: #fff;
  border: none;
  padding: 12px 36px;
  border-radius: 100px;
  font-family: 'DotGothic16', monospace;
  font-size: 16px;
  cursor: pointer;
  margin-top: 4px;
  letter-spacing: 2px;
  transition: transform .15s, box-shadow .15s;
  box-shadow: 0 4px 20px rgba(123,47,255,0.5);
}
#overlay button:active { transform: scale(0.95); }

#lives-row {
  display: flex;
  gap: 4px;
  align-items: center;
  color: #ff6ee7;
  font-size: 20px;
}
</style>
</head>
<body>

<div id="header">
  <div id="title">単位クラッシャー</div>
  <div id="score-area">
    スコア <span id="scoreVal">0</span><br>
    単位 <span id="creditVal">0</span> / 20
  </div>
</div>

<div id="canvas-wrap">
  <canvas id="c"></canvas>
  <div id="overlay">
    <h2>単位クラッシャー</h2>
    <p>全20単位を取得してクリア！<br>アイテム🎁でパドル拡大<br>タッチ or マウスで操作</p>
    <div id="lives-row">❤️❤️❤️</div>
    <button id="startBtn">ゲームスタート</button>
  </div>
</div>

<script>
(function(){
  const canvas = document.getElementById('c');
  const ctx = canvas.getContext('2d');
  const overlay = document.getElementById('overlay');
  const scoreEl = document.getElementById('scoreVal');
  const creditEl = document.getElementById('creditVal');
  const livesRow = document.getElementById('lives-row');
  const startBtn = document.getElementById('startBtn');
  const wrap = document.getElementById('canvas-wrap');

  // Canvas logical size
  const W = 400, H = 600;
  canvas.width = W; canvas.height = H;

  // ---------- CONFIG ----------
  const ROWS = 4, COLS = 5;
  const BW = 62, BH = 26, BPAD = 4;
  const BALL_R = 8;
  const PAD_H = 12, PAD_W_BASE = 80;
  const INIT_SPEED = 5;
  const SPEED_INC = 0.18; // per block destroyed
  const ITEM_CHANCE = 0.25; // 25% drop chance
  const ITEM_R = 10;
  const MAX_LIVES = 3;

  // Rainbow palette (20 blocks = 4 rows × 5 cols)
  const RAINBOW = [
    ['#ff4d4d','#ff7043','#ffa726','#ffee58','#a5d65c'],
    ['#4caf78','#26c6da','#42a5f5','#7e57c2','#ec407a'],
    ['#ff6f61','#ffd166','#06d6a0','#118ab2','#ef476f'],
    ['#f72585','#7209b7','#3a86ff','#06d6a0','#fb8500'],
  ];

  // Particle pool
  let particles = [];
  let items = [];
  let explosions = []; // block explosion squares

  // ---------- STATE ----------
  let state = 'idle'; // idle | playing | paused | gameover | clear
  let score = 0, credits = 0, lives = MAX_LIVES;
  let blocks = [], ball = {}, paddle = {};
  let speed = INIT_SPEED;
  let blocksLeft = 0;
  let padW = PAD_W_BASE;
  let padBigTimer = 0;
  let animId = null;

  // ---------- INIT ----------
  function initGame() {
    score = 0; credits = 0; lives = MAX_LIVES;
    speed = INIT_SPEED;
    padW = PAD_W_BASE;
    padBigTimer = 0;
    particles = []; items = []; explosions = [];
    updateHUD();

    // Paddle
    paddle = { x: W / 2 - padW / 2, y: H - 30, w: padW, h: PAD_H };

    // Ball
    resetBall();

    // Blocks
    blocks = [];
    const totalW = COLS * BW + (COLS - 1) * BPAD;
    const startX = (W - totalW) / 2;
    const startY = 60;
    const subjects = [
      '数学','英語','物理','化学','哲学',
      '心理','歴史','経済','法学','統計',
      '情報','倫理','地理','音楽','美術',
      '体育','医学','工学','農学','天文',
    ];
    let idx = 0;
    for (let r = 0; r < ROWS; r++) {
      for (let c = 0; c < COLS; c++) {
        blocks.push({
          x: startX + c * (BW + BPAD),
          y: startY + r * (BH + BPAD),
          w: BW, h: BH,
          color: RAINBOW[r][c],
          alive: true,
          label: subjects[idx++],
          shake: 0,
        });
      }
    }
    blocksLeft = blocks.length;
    state = 'playing';
    overlay.style.display = 'none';
  }

  function resetBall() {
    ball = {
      x: W / 2, y: H - 80,
      dx: (Math.random() > 0.5 ? 1 : -1) * speed * 0.7,
      dy: -speed * 0.9,
    };
    // Normalize to exact speed
    normalizeBall();
  }

  function normalizeBall() {
    const spd = Math.hypot(ball.dx, ball.dy);
    ball.dx = ball.dx / spd * speed;
    ball.dy = ball.dy / spd * speed;
  }

  // ---------- HUD ----------
  function updateHUD() {
    scoreEl.textContent = score;
    creditEl.textContent = credits;
    livesRow.textContent = '❤️'.repeat(Math.max(0, lives));
  }

  // ---------- DRAWING ----------
  function drawBG() {
    ctx.fillStyle = '#0a0a18';
    ctx.fillRect(0, 0, W, H);
    // subtle grid
    ctx.strokeStyle = 'rgba(255,255,255,0.025)';
    ctx.lineWidth = 0.5;
    for (let x = 0; x < W; x += 40) { ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,H); ctx.stroke(); }
    for (let y = 0; y < H; y += 40) { ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(W,y); ctx.stroke(); }
  }

  function drawBlocks() {
    blocks.forEach(b => {
      if (!b.alive) return;
      const ox = b.shake > 0 ? (Math.random() - 0.5) * 4 : 0;
      const oy = b.shake > 0 ? (Math.random() - 0.5) * 4 : 0;
      if (b.shake > 0) b.shake--;

      // Shadow glow
      ctx.shadowColor = b.color;
      ctx.shadowBlur = 8;

      // Rounded rect fill
      roundRect(ctx, b.x + ox, b.y + oy, b.w, b.h, 6);
      ctx.fillStyle = b.color;
      ctx.fill();

      // Shine strip
      ctx.shadowBlur = 0;
      ctx.fillStyle = 'rgba(255,255,255,0.18)';
      roundRect(ctx, b.x + ox + 4, b.y + oy + 3, b.w - 8, 5, 3);
      ctx.fill();

      // Label
      ctx.fillStyle = 'rgba(0,0,0,0.75)';
      ctx.font = 'bold 10px "DotGothic16", monospace';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText(b.label, b.x + ox + b.w / 2, b.y + oy + b.h / 2);
      ctx.shadowBlur = 0;
    });
  }

  function drawPaddle() {
    const g = ctx.createLinearGradient(paddle.x, 0, paddle.x + paddle.w, 0);
    g.addColorStop(0, '#ff6ee7');
    g.addColorStop(0.5, '#7ee8ff');
    g.addColorStop(1, '#ffe96e');
    ctx.shadowColor = '#7ee8ff';
    ctx.shadowBlur = 14;
    roundRect(ctx, paddle.x, paddle.y, paddle.w, paddle.h, 7);
    ctx.fillStyle = g;
    ctx.fill();
    ctx.shadowBlur = 0;
    // Big mode glow
    if (padBigTimer > 0) {
      ctx.strokeStyle = '#fff';
      ctx.lineWidth = 1.5;
      ctx.stroke();
    }
  }

  function drawBall() {
    // Trail
    ctx.shadowColor = '#fff';
    ctx.shadowBlur = 18;
    ctx.beginPath();
    ctx.arc(ball.x, ball.y, BALL_R, 0, Math.PI * 2);
    ctx.fillStyle = '#ffffff';
    ctx.fill();
    ctx.shadowBlur = 0;
    // Core highlight
    ctx.beginPath();
    ctx.arc(ball.x - 2, ball.y - 2, BALL_R * 0.35, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(255,255,255,0.6)';
    ctx.fill();
  }

  function drawItems() {
    items.forEach(it => {
      ctx.shadowColor = '#ffe96e';
      ctx.shadowBlur = 12;
      ctx.beginPath();
      ctx.arc(it.x, it.y, ITEM_R, 0, Math.PI * 2);
      ctx.fillStyle = '#ffe96e';
      ctx.fill();
      ctx.shadowBlur = 0;
      ctx.font = '12px serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('🎁', it.x, it.y + 1);
    });
  }

  function drawParticles() {
    particles.forEach(p => {
      ctx.globalAlpha = p.life;
      ctx.fillStyle = p.color;
      ctx.fillRect(p.x - p.size/2, p.y - p.size/2, p.size, p.size);
    });
    ctx.globalAlpha = 1;
  }

  function drawExplosions() {
    explosions.forEach(e => {
      ctx.globalAlpha = e.life;
      ctx.shadowColor = e.color;
      ctx.shadowBlur = 6;
      ctx.strokeStyle = e.color;
      ctx.lineWidth = 1.5;
      roundRect(ctx, e.x - e.r, e.y - e.r, e.r * 2, e.h * e.r / 14, 4);
      ctx.stroke();
      ctx.shadowBlur = 0;
    });
    ctx.globalAlpha = 1;
  }

  // ---------- UTILS ----------
  function roundRect(c, x, y, w, h, r) {
    c.beginPath();
    c.moveTo(x + r, y);
    c.lineTo(x + w - r, y);
    c.quadraticCurveTo(x + w, y, x + w, y + r);
    c.lineTo(x + w, y + h - r);
    c.quadraticCurveTo(x + w, y + h, x + w - r, y + h);
    c.lineTo(x + r, y + h);
    c.quadraticCurveTo(x, y + h, x, y + h - r);
    c.lineTo(x, y + r);
    c.quadraticCurveTo(x, y, x + r, y);
    c.closePath();
  }

  function spawnParticles(x, y, color) {
    for (let i = 0; i < 14; i++) {
      const angle = Math.random() * Math.PI * 2;
      const spd = 2 + Math.random() * 4;
      particles.push({
        x, y,
        vx: Math.cos(angle) * spd,
        vy: Math.sin(angle) * spd,
        color,
        size: 3 + Math.random() * 4,
        life: 1,
      });
    }
  }

  function spawnExplosion(b) {
    for (let i = 0; i < 6; i++) {
      explosions.push({
        x: b.x + b.w / 2,
        y: b.y + b.h / 2,
        r: (i + 1) * 5,
        h: b.h,
        color: b.color,
        life: 1,
      });
    }
  }

  function showNotif(text) {
    const el = document.createElement('div');
    el.className = 'notif';
    el.textContent = text;
    wrap.appendChild(el);
    setTimeout(() => el.remove(), 1700);
  }

  // ---------- COLLISION ----------
  function ballBlockCollision() {
    for (let b of blocks) {
      if (!b.alive) continue;
      if (ball.x + BALL_R < b.x || ball.x - BALL_R > b.x + b.w) continue;
      if (ball.y + BALL_R < b.y || ball.y - BALL_R > b.y + b.h) continue;

      // Hit! determine side
      const overlapL = (ball.x + BALL_R) - b.x;
      const overlapR = (b.x + b.w) - (ball.x - BALL_R);
      const overlapT = (ball.y + BALL_R) - b.y;
      const overlapB = (b.y + b.h) - (ball.y - BALL_R);
      const minH = Math.min(overlapL, overlapR);
      const minV = Math.min(overlapT, overlapB);
      if (minH < minV) ball.dx *= -1; else ball.dy *= -1;

      b.alive = false;
      blocksLeft--;
      credits++;
      score += 10;
      speed += SPEED_INC;
      normalizeBall();
      updateHUD();

      spawnParticles(b.x + b.w / 2, b.y + b.h / 2, b.color);
      spawnExplosion(b);
      showNotif('2単位ゲット！');

      // Item drop
      if (Math.random() < ITEM_CHANCE) {
        items.push({ x: b.x + b.w / 2, y: b.y + b.h / 2, vy: 2 });
      }

      if (blocksLeft === 0) { state = 'clear'; showEndScreen(true); }
      return;
    }
  }

  function updateItems() {
    items = items.filter(it => {
      it.y += it.vy;
      // catch by paddle
      if (it.y + ITEM_R > paddle.y && it.y - ITEM_R < paddle.y + paddle.h &&
          it.x > paddle.x && it.x < paddle.x + paddle.w) {
        padBigTimer = 300;
        showNotif('パドル拡大！');
        return false;
      }
      return it.y < H + ITEM_R;
    });
  }

  // ---------- MAIN LOOP ----------
  let lastTime = 0;
  function loop(ts) {
    if (state !== 'playing') return;
    animId = requestAnimationFrame(loop);

    drawBG();

    // Update paddle size
    if (padBigTimer > 0) {
      padBigTimer--;
      paddle.w = PAD_W_BASE * 1.7;
    } else {
      paddle.w = PAD_W_BASE;
    }

    // Ball movement
    ball.x += ball.dx;
    ball.y += ball.dy;

    // Wall bounces
    if (ball.x - BALL_R < 0) { ball.x = BALL_R; ball.dx = Math.abs(ball.dx); }
    if (ball.x + BALL_R > W) { ball.x = W - BALL_R; ball.dx = -Math.abs(ball.dx); }
    if (ball.y - BALL_R < 0) { ball.y = BALL_R; ball.dy = Math.abs(ball.dy); }

    // Paddle collision
    if (ball.dy > 0 &&
        ball.y + BALL_R >= paddle.y &&
        ball.y + BALL_R <= paddle.y + paddle.h + 4 &&
        ball.x >= paddle.x - 2 &&
        ball.x <= paddle.x + paddle.w + 2) {
      ball.dy = -Math.abs(ball.dy);
      // Angle by hit position
      const rel = (ball.x - (paddle.x + paddle.w / 2)) / (paddle.w / 2);
      ball.dx = rel * speed * 0.9;
      normalizeBall();
    }

    // Bottom = life lost
    if (ball.y - BALL_R > H) {
      lives--;
      updateHUD();
      if (lives <= 0) { state = 'gameover'; showEndScreen(false); return; }
      resetBall();
    }

    ballBlockCollision();
    updateItems();

    // Update particles
    particles = particles.filter(p => {
      p.x += p.vx; p.y += p.vy; p.vy += 0.12;
      p.life -= 0.03;
      return p.life > 0;
    });

    // Update explosions
    explosions = explosions.filter(e => {
      e.r += 1.5; e.life -= 0.07;
      return e.life > 0;
    });

    // Draw everything
    drawExplosions();
    drawBlocks();
    drawItems();
    drawParticles();
    drawPaddle();
    drawBall();

    // Speed indicator
    ctx.fillStyle = 'rgba(255,255,255,0.25)';
    ctx.font = '10px "DotGothic16"';
    ctx.textAlign = 'right';
    ctx.textBaseline = 'bottom';
    ctx.fillText('SPD ' + speed.toFixed(1), W - 8, H - 6);
  }

  // ---------- END SCREENS ----------
  function showEndScreen(win) {
    cancelAnimationFrame(animId);
    overlay.style.display = 'flex';
    overlay.innerHTML = '';

    const h2 = document.createElement('h2');
    h2.textContent = win ? '🎓 卒業おめでとう！' : '💀 留年確定…';
    overlay.appendChild(h2);

    const p = document.createElement('p');
    p.innerHTML = win
      ? `全20単位を取得しました！<br>スコア: <b>${score}</b> pts`
      : `取得単位: <b>${credits}</b> / 20<br>スコア: <b>${score}</b> pts`;
    overlay.appendChild(p);

    const btn = document.createElement('button');
    btn.textContent = win ? 'もう一度挑む' : 'リトライ';
    btn.addEventListener('click', () => { initGame(); loop(0); });
    overlay.appendChild(btn);
  }

  // ---------- CONTROLS ----------
  function movePaddle(clientX) {
    const rect = canvas.getBoundingClientRect();
    const scale = W / rect.width;
    const x = (clientX - rect.left) * scale;
    paddle.x = Math.max(0, Math.min(W - paddle.w, x - paddle.w / 2));
  }

  canvas.addEventListener('mousemove', e => { if (state === 'playing') movePaddle(e.clientX); });
  canvas.addEventListener('touchmove', e => {
    e.preventDefault();
    if (state === 'playing') movePaddle(e.touches[0].clientX);
  }, { passive: false });
  canvas.addEventListener('touchstart', e => {
    e.preventDefault();
    if (state === 'playing') movePaddle(e.touches[0].clientX);
  }, { passive: false });

  // ---------- START ----------
  startBtn.addEventListener('click', () => {
    initGame();
    animId = requestAnimationFrame(loop);
  });

  // Draw static background while idle
  drawBG();

})();
</script>
</body>
</html>
