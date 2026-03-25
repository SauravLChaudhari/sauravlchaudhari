<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Saurav L. Chaudhari — Hyperdrive Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
  :root {
    --cyan: #00FFFF;
    --magenta: #FF00FF;
    --green: #00FF88;
    --amber: #FFAA00;
    --yellow: #FFFF00;
    --blue: #0066FF;
    --bg: #030310;
    --bg2: #06061A;
    --panel: rgba(0,255,255,0.03);
    --border: rgba(0,255,255,0.15);
    --glow-c: 0 0 20px rgba(0,255,255,0.4);
    --glow-m: 0 0 20px rgba(255,0,255,0.4);
    --glow-g: 0 0 20px rgba(0,255,136,0.4);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--cyan);
    font-family: 'Rajdhani', sans-serif;
    font-weight: 400;
    min-height: 100vh;
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ── SCANLINES OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.08) 2px,
      rgba(0,0,0,0.08) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* ── GRID BACKGROUND ── */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,255,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── PARTICLE CANVAS ── */
  #particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 1;
  }

  /* ── WRAPPER ── */
  .wrapper {
    position: relative;
    z-index: 2;
    max-width: 1200px;
    margin: 0 auto;
    padding: 40px 20px 80px;
  }

  /* ── HERO HEADER ── */
  .hero {
    text-align: center;
    padding: 60px 0 50px;
    position: relative;
  }

  .hero-eyebrow {
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    letter-spacing: 6px;
    color: var(--magenta);
    text-transform: uppercase;
    margin-bottom: 16px;
    animation: fadeSlideDown 0.8s ease both;
  }

  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(32px, 6vw, 72px);
    font-weight: 900;
    line-height: 1.05;
    letter-spacing: 2px;
    background: linear-gradient(135deg, var(--cyan) 0%, var(--magenta) 50%, var(--cyan) 100%);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: gradientShift 4s ease infinite, fadeSlideDown 0.8s 0.1s ease both;
    text-shadow: none;
    filter: drop-shadow(0 0 30px rgba(0,255,255,0.5));
  }

  .hero-sub {
    font-family: 'Share Tech Mono', monospace;
    font-size: 13px;
    letter-spacing: 4px;
    color: rgba(0,255,255,0.6);
    margin-top: 14px;
    animation: fadeSlideDown 0.8s 0.2s ease both;
  }

  .hero-line {
    width: 200px;
    height: 1px;
    margin: 28px auto;
    background: linear-gradient(90deg, transparent, var(--cyan), var(--magenta), var(--cyan), transparent);
    animation: fadeSlideDown 0.8s 0.3s ease both, lineGlow 2s ease-in-out infinite alternate;
  }

  .badge-row {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 24px;
    animation: fadeSlideDown 0.8s 0.4s ease both;
  }

  .badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    padding: 5px 14px;
    border: 1px solid;
    border-radius: 2px;
    text-transform: uppercase;
  }
  .badge-c { border-color: var(--cyan); color: var(--cyan); }
  .badge-m { border-color: var(--magenta); color: var(--magenta); }
  .badge-g { border-color: var(--green); color: var(--green); }
  .badge-a { border-color: var(--amber); color: var(--amber); }

  /* ── SECTION TITLE ── */
  .section-header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 32px;
  }

  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--cyan);
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--cyan), transparent);
    opacity: 0.3;
  }

  .section-num {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: var(--magenta);
    opacity: 0.7;
  }

  /* ── PANEL ── */
  .panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 32px;
    position: relative;
    backdrop-filter: blur(4px);
    transition: border-color 0.3s, box-shadow 0.3s;
    margin-bottom: 28px;
  }

  .panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 40px; height: 2px;
    background: var(--cyan);
  }

  .panel::after {
    content: '';
    position: absolute;
    bottom: 0; right: 0;
    width: 40px; height: 2px;
    background: var(--magenta);
  }

  .panel:hover {
    border-color: rgba(0,255,255,0.35);
    box-shadow: var(--glow-c);
  }

  /* ── CHART GRID ── */
  .chart-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 28px;
    margin-bottom: 28px;
  }

  @media (max-width: 768px) {
    .chart-grid { grid-template-columns: 1fr; }
  }

  .chart-panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px 24px;
    position: relative;
    transition: border-color 0.3s, box-shadow 0.3s;
  }

  .chart-panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 30px; height: 2px;
    background: var(--cyan);
  }

  .chart-panel::after {
    content: '';
    position: absolute;
    bottom: 0; right: 0;
    width: 30px; height: 2px;
    background: var(--magenta);
  }

  .chart-panel:hover {
    border-color: rgba(0,255,255,0.35);
    box-shadow: var(--glow-c);
  }

  .chart-title {
    font-family: 'Orbitron', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--cyan);
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .chart-title-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--magenta);
    box-shadow: var(--glow-m);
    animation: pulse 2s infinite;
  }

  canvas { max-width: 100%; }

  /* ── SKILLS BARS ── */
  .skill-bar-wrap {
    display: flex;
    flex-direction: column;
    gap: 18px;
  }

  .skill-item {
    display: flex;
    flex-direction: column;
    gap: 7px;
  }

  .skill-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .skill-name {
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    letter-spacing: 2px;
    color: var(--cyan);
  }

  .skill-pct {
    font-family: 'Orbitron', monospace;
    font-size: 11px;
    font-weight: 700;
    color: var(--magenta);
  }

  .skill-track {
    height: 5px;
    background: rgba(0,255,255,0.08);
    border-radius: 0;
    overflow: hidden;
    position: relative;
  }

  .skill-fill {
    height: 100%;
    border-radius: 0;
    position: relative;
    width: 0;
    transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .skill-fill::after {
    content: '';
    position: absolute;
    right: 0; top: 0;
    height: 100%;
    width: 20px;
    background: white;
    opacity: 0.6;
    filter: blur(3px);
  }

  /* ── PHILOSOPHY QUADS ── */
  .quads {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  @media (max-width: 640px) { .quads { grid-template-columns: 1fr; } }

  .quad {
    padding: 24px 20px;
    border: 1px solid;
    border-radius: 4px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .quad:hover {
    transform: translateY(-3px);
  }

  .quad-c { border-color: var(--cyan); background: rgba(0,255,255,0.04); }
  .quad-m { border-color: var(--magenta); background: rgba(255,0,255,0.04); }
  .quad-y { border-color: var(--yellow); background: rgba(255,255,0,0.04); }
  .quad-b { border-color: #00AAFF; background: rgba(0,170,255,0.04); }

  .quad-c:hover { box-shadow: var(--glow-c); }
  .quad-m:hover { box-shadow: var(--glow-m); }
  .quad-y:hover { box-shadow: 0 0 20px rgba(255,255,0,0.4); }
  .quad-b:hover { box-shadow: 0 0 20px rgba(0,170,255,0.4); }

  .quad-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 9px;
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 10px;
    opacity: 0.6;
  }

  .quad-title {
    font-family: 'Orbitron', monospace;
    font-size: 12px;
    font-weight: 700;
    line-height: 1.4;
    margin-bottom: 8px;
  }

  .quad-c .quad-title { color: var(--cyan); }
  .quad-m .quad-title { color: var(--magenta); }
  .quad-y .quad-title { color: var(--yellow); }
  .quad-b .quad-title { color: #00AAFF; }

  .quad-desc {
    font-size: 13px;
    font-weight: 300;
    color: rgba(255,255,255,0.5);
  }

  .quad-corner {
    position: absolute;
    bottom: 12px; right: 16px;
    font-family: 'Orbitron', monospace;
    font-size: 36px;
    font-weight: 900;
    opacity: 0.06;
  }

  /* ── PHILOSOPHY QUOTE ── */
  .quote-block {
    text-align: center;
    padding: 48px 32px;
    position: relative;
  }

  .quote-text {
    font-family: 'Rajdhani', sans-serif;
    font-size: clamp(18px, 3vw, 26px);
    font-weight: 300;
    font-style: italic;
    color: rgba(0,255,255,0.8);
    line-height: 1.5;
    max-width: 700px;
    margin: 0 auto;
    letter-spacing: 1px;
  }

  .quote-mark {
    font-family: 'Orbitron', monospace;
    font-size: 60px;
    line-height: 0;
    color: var(--magenta);
    opacity: 0.3;
    vertical-align: -20px;
  }

  /* ── GITHUB STATS ── */
  .github-row {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
    margin-bottom: 28px;
  }

  @media (max-width: 768px) { .github-row { grid-template-columns: 1fr; } }

  .stat-card {
    padding: 24px 20px;
    background: rgba(0,255,255,0.03);
    border: 1px solid rgba(0,255,255,0.12);
    border-radius: 4px;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
    position: relative;
    overflow: hidden;
  }

  .stat-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--glow-c);
  }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  }

  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 36px;
    font-weight: 900;
    color: var(--cyan);
    display: block;
    filter: drop-shadow(0 0 10px rgba(0,255,255,0.6));
    animation: counter 2s ease both;
  }

  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    color: rgba(0,255,255,0.5);
    text-transform: uppercase;
    margin-top: 6px;
    display: block;
  }

  /* ── ACTIVITY FEED ── */
  .activity-list {
    display: flex;
    flex-direction: column;
    gap: 0;
  }

  .activity-item {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 14px 0;
    border-bottom: 1px solid rgba(0,255,255,0.06);
    transition: background 0.2s;
  }

  .activity-item:last-child { border-bottom: none; }

  .activity-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  .activity-month {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    color: rgba(0,255,255,0.5);
    width: 34px;
    flex-shrink: 0;
  }

  .activity-bar-wrap {
    flex: 1;
    height: 3px;
    background: rgba(0,255,255,0.06);
    border-radius: 0;
    overflow: hidden;
  }

  .activity-bar-fill {
    height: 100%;
    border-radius: 0;
    width: 0;
    transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .activity-count {
    font-family: 'Orbitron', monospace;
    font-size: 11px;
    font-weight: 700;
    width: 28px;
    text-align: right;
    flex-shrink: 0;
  }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    padding: 40px 0 20px;
    border-top: 1px solid rgba(0,255,255,0.08);
    margin-top: 60px;
  }

  .footer-text {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    color: rgba(0,255,255,0.25);
    text-transform: uppercase;
  }

  .footer-dot {
    display: inline-block;
    width: 4px; height: 4px;
    border-radius: 50%;
    background: var(--magenta);
    margin: 0 8px;
    vertical-align: middle;
    animation: pulse 2s infinite;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeSlideDown {
    from { opacity: 0; transform: translateY(-20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes gradientShift {
    0%   { background-position: 0% 50%; }
    50%  { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  @keyframes lineGlow {
    from { opacity: 0.5; }
    to   { opacity: 1; }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%       { opacity: 0.4; transform: scale(0.7); }
  }

  @keyframes blink {
    0%, 49% { opacity: 1; }
    50%, 100% { opacity: 0; }
  }

  /* ── CURSOR BLINK ── */
  .cursor {
    display: inline-block;
    width: 8px; height: 16px;
    background: var(--cyan);
    vertical-align: middle;
    margin-left: 4px;
    animation: blink 1s step-end infinite;
  }

  /* ── TERMINAL PROMPT ── */
  .terminal {
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    color: rgba(0,255,255,0.5);
    margin-bottom: 6px;
    letter-spacing: 1px;
  }

  .terminal .prompt { color: var(--green); }
  .terminal .path   { color: var(--magenta); }

  /* reveal on scroll */
  .reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<div class="wrapper">

  <!-- ══ HERO ══ -->
  <header class="hero">
    <div class="hero-eyebrow">// SYSTEM BOOT — PORTFOLIO INITIALIZED</div>
    <h1 class="hero-name">SAURAV L. CHAUDHARI</h1>
    <div class="hero-sub">ENGINEERING ARSENAL @ HYPERSONIC VELOCITY <span class="cursor"></span></div>
    <div class="hero-line"></div>
    <div class="badge-row">
      <span class="badge badge-c">Data Science</span>
      <span class="badge badge-m">Deep Learning</span>
      <span class="badge badge-g">Signal Processing</span>
      <span class="badge badge-a">Edge AI</span>
      <span class="badge badge-c">Cloud / DevOps</span>
    </div>
  </header>

  <!-- ══ GITHUB STATS ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">01</span>
      <div class="section-line"></div>
      <div class="section-title">System Metrics</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="github-row">
      <div class="stat-card">
        <span class="stat-num" data-target="847">0</span>
        <span class="stat-label">Total Commits</span>
      </div>
      <div class="stat-card">
        <span class="stat-num" data-target="24">0</span>
        <span class="stat-label">Repositories</span>
      </div>
      <div class="stat-card">
        <span class="stat-num" data-target="312">0</span>
        <span class="stat-label">Contribution Days</span>
      </div>
    </div>
  </section>

  <!-- ══ CHARTS ROW 1 ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">02</span>
      <div class="section-line"></div>
      <div class="section-title">Tech Stack Distribution</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="chart-grid">
      <div class="chart-panel">
        <div class="chart-title"><span class="chart-title-dot"></span>Arsenal Breakdown</div>
        <canvas id="pieChart" height="280"></canvas>
      </div>
      <div class="chart-panel">
        <div class="chart-title"><span class="chart-title-dot" style="background:var(--green)"></span>Core Language Mastery</div>
        <canvas id="barChart" height="280"></canvas>
      </div>
    </div>
  </section>

  <!-- ══ SKILLS BARS ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">03</span>
      <div class="section-line"></div>
      <div class="section-title">Proficiency Matrix</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="panel">
      <div class="terminal"><span class="prompt">$</span> <span class="path">~/skills</span> run proficiency_scan.sh</div>
      <br/>
      <div class="skill-bar-wrap" id="skillBars">
        <!-- injected by JS -->
      </div>
    </div>
  </section>

  <!-- ══ RADAR ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">04</span>
      <div class="section-line"></div>
      <div class="section-title">360° Edge Capability</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="chart-panel" style="max-width:600px; margin:0 auto;">
      <div class="chart-title"><span class="chart-title-dot" style="background:var(--amber)"></span>Specialized Skills Radar</div>
      <canvas id="radarChart" height="380"></canvas>
    </div>
  </section>

  <!-- ══ ACTIVITY ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">05</span>
      <div class="section-line"></div>
      <div class="section-title">Monthly Code Pulse</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="panel">
      <div class="terminal"><span class="prompt">$</span> git log --format="%aI" | datamash</div>
      <br/>
      <div class="activity-list" id="activityList"></div>
    </div>
  </section>

  <!-- ══ PHILOSOPHY QUADS ══ -->
  <section class="reveal">
    <div class="section-header">
      <span class="section-num">06</span>
      <div class="section-line"></div>
      <div class="section-title">Engineering Philosophy</div>
      <div class="section-line" style="background:linear-gradient(90deg,transparent,var(--cyan));"></div>
    </div>
    <div class="quads">
      <div class="quad quad-c">
        <div class="quad-label">High Impact</div>
        <div class="quad-title">⚡ Signal Processing + ML Fusion</div>
        <div class="quad-desc">Where raw signals meet learned representations — turning noise into intelligence.</div>
        <div class="quad-corner">⚡</div>
      </div>
      <div class="quad quad-m">
        <div class="quad-label">High Focus</div>
        <div class="quad-title">🏗️ End-to-End Systems</div>
        <div class="quad-desc">From data ingestion to deployed inference — no handoffs, full ownership.</div>
        <div class="quad-corner">🏗</div>
      </div>
      <div class="quad quad-y">
        <div class="quad-label">Core Strength</div>
        <div class="quad-title">🔬 Practical AI</div>
        <div class="quad-desc">Real-world data is noisy, partial, and adversarial. Theory meets battlefield here.</div>
        <div class="quad-corner">🔬</div>
      </div>
      <div class="quad quad-b">
        <div class="quad-label">Production Ready</div>
        <div class="quad-title">☁️ Scalable Infra + Hardware Edge</div>
        <div class="quad-desc">Distributed pipelines to microcontrollers — scale in both directions.</div>
        <div class="quad-corner">☁</div>
      </div>
    </div>
  </section>

  <!-- ══ QUOTE ══ -->
  <section class="reveal">
    <div class="panel quote-block">
      <div class="quote-text">
        <span class="quote-mark">"</span>
        Build systems that work in the real world — noisy, imperfect, and scalable.
        <span class="quote-mark">"</span>
      </div>
    </div>
  </section>

  <!-- ══ FOOTER ══ -->
  <footer class="footer">
    <div class="footer-text">
      SAURAV L. CHAUDHARI
      <span class="footer-dot"></span>
      HYPERDRIVE PORTFOLIO
      <span class="footer-dot"></span>
      NEON-CODED
    </div>
  </footer>

</div><!-- /wrapper -->

<script>
/* ══════════════════════════════════════
   PARTICLES
══════════════════════════════════════ */
(function(){
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');
  let W, H, particles = [];

  function resize(){
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }

  function Particle(){
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.size = Math.random() * 1.2 + 0.3;
    this.vx = (Math.random() - 0.5) * 0.3;
    this.vy = (Math.random() - 0.5) * 0.3;
    this.alpha = Math.random() * 0.4 + 0.1;
    this.color = Math.random() > 0.5 ? '0,255,255' : '255,0,255';
  }

  Particle.prototype.update = function(){
    this.x += this.vx; this.y += this.vy;
    if(this.x < 0) this.x = W;
    if(this.x > W) this.x = 0;
    if(this.y < 0) this.y = H;
    if(this.y > H) this.y = 0;
  };

  Particle.prototype.draw = function(){
    ctx.save();
    ctx.globalAlpha = this.alpha;
    ctx.fillStyle = `rgba(${this.color},1)`;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fill();
    ctx.restore();
  };

  resize();
  window.addEventListener('resize', resize);

  for(let i = 0; i < 80; i++) particles.push(new Particle());

  function loop(){
    ctx.clearRect(0, 0, W, H);
    particles.forEach(p => { p.update(); p.draw(); });
    // Draw connections
    for(let i = 0; i < particles.length; i++){
      for(let j = i+1; j < particles.length; j++){
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const dist = Math.sqrt(dx*dx + dy*dy);
        if(dist < 120){
          ctx.save();
          ctx.globalAlpha = (1 - dist/120) * 0.12;
          ctx.strokeStyle = '#00FFFF';
          ctx.lineWidth = 0.5;
          ctx.beginPath();
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.stroke();
          ctx.restore();
        }
      }
    }
    requestAnimationFrame(loop);
  }
  loop();
})();

/* ══════════════════════════════════════
   CHART.JS DEFAULTS
══════════════════════════════════════ */
Chart.defaults.color = 'rgba(0,255,255,0.7)';
Chart.defaults.font.family = "'Share Tech Mono', monospace";

/* ── PIE CHART ── */
new Chart(document.getElementById('pieChart'), {
  type: 'doughnut',
  data: {
    labels: ['Data Science & ML','Core Languages','Deep Learning','Tools & Hardware','Cloud & DevOps'],
    datasets: [{
      data: [30, 20, 20, 15, 15],
      backgroundColor: [
        'rgba(255,0,255,0.7)',
        'rgba(0,255,255,0.7)',
        'rgba(0,255,136,0.7)',
        'rgba(255,170,0,0.7)',
        'rgba(255,255,0,0.7)',
      ],
      borderColor: '#030310',
      borderWidth: 3,
      hoverOffset: 10,
    }]
  },
  options: {
    responsive: true,
    cutout: '58%',
    plugins: {
      legend: {
        position: 'bottom',
        labels: {
          color: 'rgba(0,255,255,0.8)',
          font: { size: 10, family: "'Share Tech Mono', monospace" },
          padding: 14,
          boxWidth: 10, boxHeight: 10,
          usePointStyle: true,
        }
      },
      tooltip: {
        backgroundColor: 'rgba(6,6,26,0.95)',
        borderColor: 'rgba(0,255,255,0.3)',
        borderWidth: 1,
        titleColor: '#00FFFF',
        bodyColor: 'rgba(255,255,255,0.8)',
      }
    },
    animation: { animateRotate: true, duration: 1400 }
  }
});

/* ── BAR CHART ── */
new Chart(document.getElementById('barChart'), {
  type: 'bar',
  data: {
    labels: ['C++', 'Python', 'R', 'HTML5'],
    datasets: [{
      label: 'Proficiency',
      data: [88, 95, 75, 65],
      backgroundColor: [
        'rgba(0,255,255,0.6)',
        'rgba(0,255,136,0.6)',
        'rgba(255,170,0,0.6)',
        'rgba(255,0,255,0.6)',
      ],
      borderColor: [
        '#00FFFF', '#00FF88', '#FFAA00', '#FF00FF',
      ],
      borderWidth: 1,
      borderRadius: 2,
    }]
  },
  options: {
    responsive: true,
    plugins: {
      legend: { display: false },
      tooltip: {
        backgroundColor: 'rgba(6,6,26,0.95)',
        borderColor: 'rgba(0,255,255,0.3)',
        borderWidth: 1,
        titleColor: '#00FFFF',
        bodyColor: 'rgba(255,255,255,0.8)',
        callbacks: { label: ctx => ` ${ctx.raw}% proficiency` }
      }
    },
    scales: {
      y: {
        min: 0, max: 100,
        grid: { color: 'rgba(0,255,255,0.05)' },
        ticks: { color: 'rgba(0,255,255,0.5)', font: { size: 11 }, callback: v => v + '%' }
      },
      x: {
        grid: { display: false },
        ticks: { color: 'rgba(0,255,255,0.8)', font: { size: 13, weight: '700' } }
      }
    },
    animation: { duration: 1400 }
  }
});

/* ── RADAR CHART ── */
new Chart(document.getElementById('radarChart'), {
  type: 'radar',
  data: {
    labels: ['Time-Series\nModeling','Physiological\nSignals','Feature\nEngineering','ML\nPipelines','Edge\nIntelligence','Distributed\nSystems'],
    datasets: [{
      label: 'Mastery',
      data: [98, 95, 92, 97, 90, 88],
      fill: true,
      backgroundColor: 'rgba(0,255,255,0.1)',
      borderColor: '#00FFFF',
      borderWidth: 2,
      pointBackgroundColor: '#FF00FF',
      pointBorderColor: '#000',
      pointRadius: 5,
      pointHoverRadius: 7,
    }]
  },
  options: {
    responsive: true,
    plugins: {
      legend: { display: false },
      tooltip: {
        backgroundColor: 'rgba(6,6,26,0.95)',
        borderColor: 'rgba(0,255,255,0.3)',
        borderWidth: 1,
        titleColor: '#00FFFF',
        bodyColor: 'rgba(255,255,255,0.8)',
      }
    },
    scales: {
      r: {
        min: 60, max: 100,
        angleLines: { color: 'rgba(0,255,255,0.08)' },
        grid: { color: 'rgba(0,255,255,0.08)' },
        pointLabels: {
          color: 'rgba(0,255,255,0.8)',
          font: { size: 11, family: "'Share Tech Mono', monospace" }
        },
        ticks: {
          color: 'rgba(0,255,255,0.4)',
          backdropColor: 'transparent',
          font: { size: 9 },
          callback: v => v + '%'
        }
      }
    },
    animation: { duration: 1400 }
  }
});

/* ══════════════════════════════════════
   SKILL BARS
══════════════════════════════════════ */
const skills = [
  { name: 'PYTHON', pct: 95, color: '#00FF88' },
  { name: 'C++', pct: 88, color: '#00FFFF' },
  { name: 'TIME-SERIES MODELING', pct: 98, color: '#FF00FF' },
  { name: 'ML PIPELINES', pct: 97, color: '#00FFFF' },
  { name: 'PHYSIOLOGICAL SIGNALS', pct: 95, color: '#FFAA00' },
  { name: 'FEATURE ENGINEERING', pct: 92, color: '#FF00FF' },
  { name: 'EDGE INTELLIGENCE', pct: 90, color: '#FFFF00' },
  { name: 'DISTRIBUTED SYSTEMS', pct: 88, color: '#00AAFF' },
  { name: 'R', pct: 75, color: '#FFAA00' },
];

const sbWrap = document.getElementById('skillBars');
skills.forEach(s => {
  sbWrap.innerHTML += `
    <div class="skill-item">
      <div class="skill-meta">
        <span class="skill-name">${s.name}</span>
        <span class="skill-pct">${s.pct}%</span>
      </div>
      <div class="skill-track">
        <div class="skill-fill" data-pct="${s.pct}" style="background:linear-gradient(90deg,${s.color}88,${s.color});"></div>
      </div>
    </div>
  `;
});

/* ══════════════════════════════════════
   ACTIVITY LIST
══════════════════════════════════════ */
const months = ['JAN','FEB','MAR','APR','MAY','JUN','JUL','AUG','SEP','OCT','NOV','DEC'];
const commits = [45,62,38,75,88,55,92,67,81,49,70,95];
const maxC = Math.max(...commits);
const colors = ['#00FFFF','#FF00FF','#00FF88','#FFAA00','#FFFF00','#00AAFF'];
const al = document.getElementById('activityList');
months.forEach((m, i) => {
  const pct = (commits[i] / maxC * 100).toFixed(1);
  const col = colors[i % colors.length];
  al.innerHTML += `
    <div class="activity-item">
      <div class="activity-dot" style="background:${col};box-shadow:0 0 6px ${col};"></div>
      <div class="activity-month">${m}</div>
      <div class="activity-bar-wrap">
        <div class="activity-bar-fill" data-pct="${pct}" style="background:linear-gradient(90deg,${col}55,${col});"></div>
      </div>
      <div class="activity-count" style="color:${col}">${commits[i]}</div>
    </div>
  `;
});

/* ══════════════════════════════════════
   COUNTER ANIMATION
══════════════════════════════════════ */
function animateCounter(el){
  const target = parseInt(el.dataset.target);
  const start = performance.now();
  const dur = 2000;
  function step(now){
    const p = Math.min((now - start) / dur, 1);
    const ease = 1 - Math.pow(1 - p, 3);
    el.textContent = Math.round(ease * target);
    if(p < 1) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

/* ══════════════════════════════════════
   INTERSECTION OBSERVER
══════════════════════════════════════ */
const io = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if(entry.isIntersecting){
      entry.target.classList.add('visible');

      // animate skill bars
      entry.target.querySelectorAll('.skill-fill[data-pct]').forEach(el => {
        el.style.width = el.dataset.pct + '%';
      });

      // animate activity bars
      entry.target.querySelectorAll('.activity-bar-fill[data-pct]').forEach(el => {
        el.style.width = el.dataset.pct + '%';
      });

      // animate counters
      entry.target.querySelectorAll('.stat-num[data-target]').forEach(el => {
        animateCounter(el);
      });
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('.reveal').forEach(el => io.observe(el));
</script>
</body>
</html>
