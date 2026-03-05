<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>ZercoDeus — GitHub Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --white: #ffffff;
    --off-white: #e0e0e0;
    --dim: #888;
    --faint: #333;
    --bg: #000000;
    --card-bg: rgba(5, 5, 5, 0.92);
    --border: rgba(255,255,255,0.12);
    --glow: rgba(255,255,255,0.08);
  }

  html, body {
    background: var(--bg);
    color: var(--white);
    font-family: 'Share Tech Mono', monospace;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  /* ── Matrix Rain ── */
  #matrix {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
  }

  /* ── Card ── */
  .card {
    position: relative;
    z-index: 10;
    width: min(760px, 96vw);
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 48px 52px 44px;
    backdrop-filter: blur(2px);
    box-shadow: 0 0 60px rgba(255,255,255,0.03), inset 0 0 40px rgba(0,0,0,0.6);
  }

  /* scanline overlay */
  .card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: repeating-linear-gradient(
      to bottom,
      transparent 0px,
      transparent 3px,
      rgba(0,0,0,0.18) 3px,
      rgba(0,0,0,0.18) 4px
    );
    border-radius: 4px;
    pointer-events: none;
    z-index: 1;
  }

  .card-inner { position: relative; z-index: 2; }

  /* ── Top bar ── */
  .topbar {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 36px;
    opacity: 0;
    animation: fadeUp 0.6s 0.2s forwards;
  }
  .dot { width: 11px; height: 11px; border-radius: 50%; }
  .dot-r { background: #3a3a3a; }
  .dot-y { background: #2e2e2e; }
  .dot-g { background: #252525; }
  .topbar-label {
    margin-left: auto;
    font-size: 11px;
    color: var(--dim);
    letter-spacing: 3px;
    text-transform: uppercase;
  }

  /* ── Prompt line ── */
  .prompt {
    font-size: 12px;
    color: var(--dim);
    letter-spacing: 1px;
    margin-bottom: 6px;
    opacity: 0;
    animation: fadeUp 0.5s 0.5s forwards;
  }
  .prompt span { color: var(--off-white); }

  /* ── Name ── */
  .name {
    font-family: 'VT323', monospace;
    font-size: clamp(52px, 9vw, 82px);
    line-height: 1;
    letter-spacing: 4px;
    color: var(--white);
    text-shadow: 0 0 30px rgba(255,255,255,0.2), 0 0 80px rgba(255,255,255,0.05);
    margin-bottom: 10px;
    opacity: 0;
    animation: fadeUp 0.7s 0.8s forwards;
  }

  /* ── Tagline decode ── */
  .tagline {
    font-size: 13.5px;
    color: var(--off-white);
    letter-spacing: 2px;
    margin-bottom: 36px;
    min-height: 20px;
    opacity: 0;
    animation: fadeUp 0.5s 1.2s forwards;
  }
  .cursor {
    display: inline-block;
    width: 9px;
    height: 14px;
    background: var(--white);
    vertical-align: middle;
    margin-left: 3px;
    animation: blink 0.9s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ── Divider ── */
  .divider {
    border: none;
    border-top: 1px solid var(--border);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeIn 0.5s 1.6s forwards;
  }

  /* ── Section title ── */
  .sec-title {
    font-size: 10px;
    letter-spacing: 4px;
    color: var(--dim);
    text-transform: uppercase;
    margin-bottom: 14px;
  }

  /* ── About ── */
  .about {
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.5s 1.8s forwards;
  }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px 24px;
  }
  .about-item {
    font-size: 12.5px;
    color: var(--off-white);
    letter-spacing: 0.5px;
    padding: 6px 0;
    border-bottom: 1px solid var(--faint);
    display: flex;
    gap: 10px;
  }
  .about-item .icon { color: var(--dim); flex-shrink: 0; }

  /* ── Stack ── */
  .stack {
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.5s 2.1s forwards;
  }
  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    letter-spacing: 1.5px;
    padding: 5px 12px;
    border: 1px solid rgba(255,255,255,0.18);
    color: var(--off-white);
    background: rgba(255,255,255,0.03);
    border-radius: 2px;
    transition: background 0.2s, border-color 0.2s;
    cursor: default;
  }
  .badge:hover {
    background: rgba(255,255,255,0.08);
    border-color: rgba(255,255,255,0.4);
  }

  /* ── Stats row ── */
  .stats {
    display: flex;
    gap: 0;
    border: 1px solid var(--border);
    border-radius: 2px;
    overflow: hidden;
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.5s 2.4s forwards;
  }
  .stat {
    flex: 1;
    padding: 16px 12px;
    text-align: center;
    border-right: 1px solid var(--border);
    transition: background 0.2s;
  }
  .stat:last-child { border-right: none; }
  .stat:hover { background: rgba(255,255,255,0.03); }
  .stat-num {
    font-family: 'VT323', monospace;
    font-size: 32px;
    color: var(--white);
    line-height: 1;
    display: block;
  }
  .stat-label {
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--dim);
    text-transform: uppercase;
    margin-top: 4px;
  }

  /* ── Connect ── */
  .connect {
    opacity: 0;
    animation: fadeUp 0.5s 2.7s forwards;
  }
  .connect-links {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }
  .connect-link {
    font-size: 11px;
    letter-spacing: 2px;
    color: var(--dim);
    text-decoration: none;
    border: 1px solid var(--faint);
    padding: 7px 16px;
    border-radius: 2px;
    transition: color 0.2s, border-color 0.2s;
    text-transform: uppercase;
  }
  .connect-link:hover {
    color: var(--white);
    border-color: rgba(255,255,255,0.5);
  }

  /* ── Footer ── */
  .footer {
    margin-top: 36px;
    padding-top: 20px;
    border-top: 1px solid var(--faint);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 10px;
    color: #444;
    letter-spacing: 2px;
    opacity: 0;
    animation: fadeIn 0.5s 3s forwards;
  }

  /* ── Animations ── */
  @keyframes fadeUp {
    from { opacity:0; transform: translateY(10px); }
    to   { opacity:1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity:0; }
    to   { opacity:1; }
  }
</style>
</head>
<body>

<canvas id="matrix"></canvas>

<div class="card">
  <div class="card-inner">

    <div class="topbar">
      <div class="dot dot-r"></div>
      <div class="dot dot-y"></div>
      <div class="dot dot-g"></div>
      <span class="topbar-label">profile.exe</span>
    </div>

    <div class="prompt">root@github:~$ <span>cat ZercoDeus/README.md</span></div>

    <div class="name">ZercoDeus</div>

    <div class="tagline" id="tagline"><span class="cursor"></span></div>

    <hr class="divider"/>

    <div class="about">
      <div class="sec-title">// about</div>
      <div class="about-grid">
        <div class="about-item"><span class="icon">▸</span> Working on full stack projects</div>
        <div class="about-item"><span class="icon">▸</span> Clean &amp; scalable architecture</div>
        <div class="about-item"><span class="icon">▸</span> Always learning something new</div>
        <div class="about-item"><span class="icon">▸</span> Building products that matter</div>
      </div>
    </div>

    <div class="stack">
      <div class="sec-title">// stack</div>
      <div class="badges">
        <span class="badge">HTML5</span>
        <span class="badge">CSS3</span>
        <span class="badge">JavaScript</span>
        <span class="badge">React</span>
        <span class="badge">Node.js</span>
        <span class="badge">Python</span>
        <span class="badge">MySQL</span>
        <span class="badge">MongoDB</span>
        <span class="badge">Docker</span>
        <span class="badge">Git</span>
      </div>
    </div>

    <div class="stats">
      <div class="stat">
        <span class="stat-num" id="c-commits">000</span>
        <div class="stat-label">Commits</div>
      </div>
      <div class="stat">
        <span class="stat-num" id="c-repos">000</span>
        <div class="stat-label">Repos</div>
      </div>
      <div class="stat">
        <span class="stat-num" id="c-prs">000</span>
        <div class="stat-label">Pull Requests</div>
      </div>
      <div class="stat">
        <span class="stat-num" id="c-stars">000</span>
        <div class="stat-label">Stars</div>
      </div>
    </div>

    <div class="connect">
      <div class="sec-title">// connect</div>
      <div class="connect-links">
        <a class="connect-link" href="https://github.com/ZercoDeus">GitHub</a>
        <a class="connect-link" href="#">LinkedIn</a>
        <a class="connect-link" href="#">Twitter</a>
        <a class="connect-link" href="#">Portfolio</a>
      </div>
    </div>

    <div class="footer">
      <span>© 2026 ZERCODEUS</span>
      <span id="uptime">SYS::ONLINE</span>
    </div>

  </div>
</div>

<script>
/* ── Matrix Rain ── */
(function(){
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');
  let W, H, cols, drops;
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%&*<>/\\|[]{}あいうえおアイウエオ';
  const fontSize = 14;

  function init(){
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
    cols = Math.floor(W / fontSize);
    drops = Array.from({length: cols}, () => Math.random() * -H/fontSize | 0);
  }

  function draw(){
    ctx.fillStyle = 'rgba(0,0,0,0.055)';
    ctx.fillRect(0,0,W,H);
    for(let i = 0; i < cols; i++){
      const y = drops[i] * fontSize;
      // head char — bright white
      ctx.fillStyle = '#ffffff';
      ctx.font = `${fontSize}px "Share Tech Mono", monospace`;
      ctx.fillText(chars[Math.random()*chars.length|0], i*fontSize, y);
      // body — dim white
      if(y > 0){
        ctx.fillStyle = 'rgba(200,200,200,0.25)';
        ctx.fillText(chars[Math.random()*chars.length|0], i*fontSize, y - fontSize);
      }
      if(y > H && Math.random() > 0.975) drops[i] = 0;
      drops[i]++;
    }
  }

  init();
  window.addEventListener('resize', init);
  setInterval(draw, 45);
})();

/* ── Decode Tagline ── */
(function(){
  const el = document.getElementById('tagline');
  const target = 'Full Stack Developer · Building clean, scalable solutions · Always learning something new';
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%&*<>/\\';
  let revealed = 0;
  let frame = 0;
  const cursor = '<span class="cursor"></span>';

  function tick(){
    if(revealed > target.length) return;
    frame++;
    let display = target.slice(0, revealed);
    // scramble the next few chars
    let noise = '';
    const ahead = Math.min(4, target.length - revealed);
    for(let i = 0; i < ahead; i++){
      noise += chars[Math.random()*chars.length|0];
    }
    el.innerHTML = display + `<span style="color:#555">${noise}</span>` + cursor;
    if(frame % 3 === 0) revealed++;
    requestAnimationFrame(tick);
  }

  setTimeout(tick, 1400);
})();

/* ── Count-up stats ── */
(function(){
  const targets = {
    'c-commits': 347,
    'c-repos':    28,
    'c-prs':      94,
    'c-stars':    61
  };
  function countUp(id, end){
    const el = document.getElementById(id);
    let val = 0;
    const step = Math.max(1, Math.floor(end/60));
    const iv = setInterval(()=>{
      val = Math.min(val + step, end);
      el.textContent = String(val).padStart(3,'0');
      if(val >= end) clearInterval(iv);
    }, 30);
  }
  setTimeout(()=>{
    Object.entries(targets).forEach(([id,end])=> countUp(id, end));
  }, 2600);
})();

/* ── Uptime clock ── */
(function(){
  const el = document.getElementById('uptime');
  const start = Date.now();
  setInterval(()=>{
    const s = Math.floor((Date.now()-start)/1000);
    const h = String(Math.floor(s/3600)).padStart(2,'0');
    const m = String(Math.floor((s%3600)/60)).padStart(2,'0');
    const ss = String(s%60).padStart(2,'0');
    el.textContent = `UPTIME::${h}:${m}:${ss}`;
  }, 1000);
})();
</script>
</body>
</html>
