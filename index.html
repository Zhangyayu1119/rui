<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Heart Beat + Particles</title>
  <style>
    :root{
      --bg1:#0b1026;
      --bg2:#170b2a;
      --heart:#ff3b6b;
      --glow:#ff7aa8;

      /* 心跳周期：1.2s = 50 BPM 的“慢周期”，但内部是双击跳（更像真实心跳） */
      --cycle: 1.2s;
      --size: 180px;
    }

    *{ box-sizing:border-box; }
    html,body{ height:100%; margin:0; }
    body{
      overflow:hidden;
      display:flex;
      align-items:center;
      justify-content:center;
      background: radial-gradient(1200px 800px at 50% 40%, rgba(255,70,130,.18), transparent 60%),
                  linear-gradient(145deg, var(--bg1), var(--bg2));
      font-family: system-ui, -apple-system, "Segoe UI", Roboto, "PingFang SC", "Microsoft YaHei", Arial, sans-serif;
      color: rgba(255,255,255,.85);
      user-select:none;
    }

    /* 粒子画布：全屏覆盖 */
    #fx{
      position:fixed;
      inset:0;
      width:100vw;
      height:100vh;
      z-index:0;
      pointer-events:none;
    }

    /* 中心容器 */
    .wrap{
      position:relative;
      z-index:1;
      display:flex;
      flex-direction:column;
      align-items:center;
      gap:18px;
      padding:24px 28px;
      border-radius:20px;
      background: rgba(255,255,255,.06);
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 60px rgba(0,0,0,.35);
    }

    /* 爱心本体：纯 CSS 形状 */
    .heart{
      width: var(--size);
      height: var(--size);
      position:relative;
      transform: rotate(45deg);
      background: var(--heart);
      border-radius: 18px;
      filter: drop-shadow(0 0 24px rgba(255, 80, 150, .35));
      cursor:pointer;

      /* 跳动动画 */
      animation: heartbeat var(--cycle) infinite;
      transform-origin: 50% 60%;
    }

    .heart::before,
    .heart::after{
      content:"";
      position:absolute;
      width: var(--size);
      height: var(--size);
      background: var(--heart);
      border-radius: 50%;
    }
    .heart::before{ left: -50%; top: 0; }
    .heart::after{ left: 0; top: -50%; }

    /* 发光边缘（微微高亮） */
    .heart::marker{ content:""; }

    /* 心跳：双击跳（强-弱-停顿）+ 轻微上下弹 */
    @keyframes heartbeat{
      0%   { transform: rotate(45deg) scale(1) translateY(0); }
      10%  { transform: rotate(45deg) scale(1.08) translateY(-2px); }
      18%  { transform: rotate(45deg) scale(0.98) translateY(0); }
      26%  { transform: rotate(45deg) scale(1.04) translateY(-1px); }
      34%  { transform: rotate(45deg) scale(1) translateY(0); }
      100% { transform: rotate(45deg) scale(1) translateY(0); }
    }

    .title{
      font-weight:700;
      letter-spacing:.5px;
      font-size:16px;
      opacity:.95;
    }
    .hint{
      font-size:12px;
      opacity:.8;
      line-height:1.4;
      text-align:center;
    }
    .pill{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 12px;
      border:1px solid rgba(255,255,255,.12);
      border-radius:999px;
      background: rgba(0,0,0,.12);
    }
    .kbd{
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace;
      font-size:12px;
      padding:2px 6px;
      border-radius:6px;
      background: rgba(255,255,255,.10);
      border:1px solid rgba(255,255,255,.12);
    }
  </style>
</head>
<body>
  <canvas id="fx"></canvas>

  <div class="wrap">
    <div class="title">跳动的爱心 + 粒子特效 ❤️✨</div>

    <div id="heart" class="heart" aria-label="heart"></div>

    <div class="hint">
      <span class="pill">点击/触摸爱心：<span class="kbd">爆发粒子</span></span><br/>
      （心跳会自动喷粒子，适合直接丢 GitHub Pages）
    </div>
  </div>

  <script>
    /***********************
     *  Canvas 粒子系统
     ***********************/
    const canvas = document.getElementById('fx');
    const ctx = canvas.getContext('2d', { alpha: true });

    const heartEl = document.getElementById('heart');

    let W = 0, H = 0, DPR = Math.max(1, Math.min(2.5, window.devicePixelRatio || 1));

    function resize(){
      W = Math.floor(window.innerWidth);
      H = Math.floor(window.innerHeight);
      canvas.width  = Math.floor(W * DPR);
      canvas.height = Math.floor(H * DPR);
      canvas.style.width = W + "px";
      canvas.style.height = H + "px";
      ctx.setTransform(DPR, 0, 0, DPR, 0, 0);
    }
    window.addEventListener('resize', resize, { passive: true });
    resize();

    // 爱心轮廓参数方程（经典心形曲线）
    // x = 16 sin^3(t), y = 13 cos(t) - 5 cos(2t) - 2 cos(3t) - cos(4t)
    function heartPoint(t){
      const s = Math.sin(t);
      const c = Math.cos(t);
      const x = 16 * s * s * s;
      const y = 13 * c - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t);
      return { x, y };
    }

    function getHeartCenter(){
      const r = heartEl.getBoundingClientRect();
      return { cx: r.left + r.width/2, cy: r.top + r.height/2, r };
    }

    const particles = [];
    const palette = [
      "rgba(255,59,107,1)",
      "rgba(255,122,168,1)",
      "rgba(255,203,221,1)",
      "rgba(255,255,255,1)"
    ];

    function rand(a,b){ return a + Math.random()*(b-a); }

    function spawnBurst(strength = 1){
      const { cx, cy, r } = getHeartCenter();

      // 根据 DOM 爱心大小自适应缩放
      const scale = (Math.min(r.width, r.height) / 40) * 1.05;

      // 粒子数量：强度越大越多
      const count = Math.floor(70 * strength);

      for(let i=0; i<count; i++){
        const t = Math.random() * Math.PI * 2;
        const p = heartPoint(t);

        // 把心形曲线映射到屏幕坐标（注意 y 方向需要翻转）
        const px = cx + p.x * scale;
        const py = cy - p.y * scale;

        // 方向：从中心指向轮廓点，再叠加随机扰动
        let dx = px - cx, dy = py - cy;
        const len = Math.hypot(dx, dy) || 1;
        dx /= len; dy /= len;

        const speed = rand(140, 360) * strength;
        const jitter = 0.65;

        particles.push({
          x: px + rand(-2, 2),
          y: py + rand(-2, 2),
          vx: (dx + rand(-jitter, jitter)) * speed / 60,
          vy: (dy + rand(-jitter, jitter)) * speed / 60,
          g: rand(220, 520) / 60,        // 重力
          drag: rand(0.985, 0.995),      // 阻尼
          life: 0,
          ttl: rand(0.7, 1.35) * (1.05/strength),
          size: rand(1.6, 3.6) * (1 + 0.25*strength),
          rot: rand(0, Math.PI*2),
          spin: rand(-6, 6),
          color: palette[Math.floor(Math.random()*palette.length)],
        });
      }
    }

    // 画“爱心粒子”（小心形）——比圆点更有味道😄
    function drawMiniHeart(x, y, s, rot, color, alpha){
      ctx.save();
      ctx.translate(x, y);
      ctx.rotate(rot);
      ctx.globalAlpha = alpha;

      ctx.fillStyle = color;
      ctx.beginPath();
      // 用贝塞尔做一个小心形（简化版）
      const k = s;
      ctx.moveTo(0, 0.35*k);
      ctx.bezierCurveTo(0, 0, -0.55*k, 0, -0.55*k, 0.35*k);
      ctx.bezierCurveTo(-0.55*k, 0.75*k, 0, 0.95*k, 0, 1.2*k);
      ctx.bezierCurveTo(0, 0.95*k, 0.55*k, 0.75*k, 0.55*k, 0.35*k);
      ctx.bezierCurveTo(0.55*k, 0, 0, 0, 0, 0.35*k);
      ctx.closePath();
      ctx.fill();

      ctx.restore();
    }

    let last = performance.now();

    function tick(now){
      const dt = Math.min(0.033, (now - last) / 1000);
      last = now;

      // 清屏（透明画布）——你也可以换成“拖影”效果
      ctx.clearRect(0, 0, W, H);

      // 更梦幻：叠加发光混合
      ctx.save();
      ctx.globalCompositeOperation = "lighter";
      ctx.shadowBlur = 14;
      ctx.shadowColor = "rgba(255,122,168,.35)";

      for(let i = particles.length - 1; i >= 0; i--){
        const p = particles[i];
        p.life += dt;

        // 更新位置
        p.vx *= Math.pow(p.drag, 60*dt);
        p.vy *= Math.pow(p.drag, 60*dt);
        p.vy += p.g * dt;

        p.x += p.vx * 60 * dt;
        p.y += p.vy * 60 * dt;

        p.rot += p.spin * dt;

        const t = p.life / p.ttl;
        const alpha = (1 - t) * (1 - 0.12*t);

        if(t >= 1){
          particles.splice(i, 1);
          continue;
        }

        // 小心形粒子
        drawMiniHeart(p.x, p.y, p.size * (1 + 0.35*t), p.rot, p.color, alpha);
      }

      ctx.restore();
      requestAnimationFrame(tick);
    }
    requestAnimationFrame(tick);

    /***********************
     *  心跳节奏：双击跳
     ***********************/
    // 周期与 CSS 对齐（默认 1200ms）
    const cycleMs = 1200;

    function startHeartBeats(){
      function loop(){
        // 强跳 + 弱跳
        spawnBurst(1.0);
        setTimeout(() => spawnBurst(0.65), 200);
        setTimeout(loop, cycleMs);
      }
      loop();
    }
    startHeartBeats();

    /***********************
     *  交互：点击爆发
     ***********************/
    function bigBoom(){
      spawnBurst(1.9);
      setTimeout(() => spawnBurst(1.2), 120);
      setTimeout(() => spawnBurst(0.9), 240);
    }

    heartEl.addEventListener('pointerdown', (e) => {
      e.preventDefault();
      bigBoom();
    });

    // 也支持空格触发（桌面端演示更方便）
    window.addEventListener('keydown', (e) => {
      if(e.code === 'Space'){
        bigBoom();
      }
    });
  </script>
</body>
</html>
