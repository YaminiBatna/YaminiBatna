<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Batna Yamini — AI & ML Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --cyan: #00C9FF;
    --green: #92FE9D;
    --dark: #050a0e;
    --card: #0a141a;
    --border: rgba(0,201,255,0.18);
    --glow: rgba(0,201,255,0.35);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--dark);
    color: #cdedf5;
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* ─── CUSTOM CURSOR ─── */
  #cursor {
    position: fixed; top: 0; left: 0; z-index: 9999;
    width: 14px; height: 14px;
    border-radius: 50%;
    background: var(--cyan);
    box-shadow: 0 0 18px var(--cyan), 0 0 40px var(--glow);
    pointer-events: none;
    transform: translate(-50%,-50%);
    transition: transform .08s, width .2s, height .2s, opacity .2s;
  }
  #cursor-ring {
    position: fixed; top: 0; left: 0; z-index: 9998;
    width: 40px; height: 40px;
    border-radius: 50%;
    border: 1.5px solid rgba(0,201,255,0.5);
    pointer-events: none;
    transform: translate(-50%,-50%);
    transition: transform .18s ease, width .3s, height .3s;
  }

  /* ─── STAR CANVAS ─── */
  #stars { position: fixed; inset: 0; z-index: 0; }

  /* ─── HERO ─── */
  .hero {
    position: relative; z-index: 1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding: 60px 24px;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 40%, rgba(0,201,255,.12) 0%, transparent 70%);
    animation: breathe 5s ease-in-out infinite;
  }
  @keyframes breathe {
    0%,100% { opacity:.7; transform: scale(1); }
    50% { opacity:1; transform: scale(1.05); }
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: .72rem; letter-spacing: .22em;
    color: var(--cyan); text-transform: uppercase;
    border: 1px solid var(--border);
    padding: 6px 18px; border-radius: 40px;
    margin-bottom: 28px;
    opacity: 0; animation: fadeUp .7s .2s forwards;
    backdrop-filter: blur(8px);
    background: rgba(0,201,255,.06);
  }

  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(2.6rem, 7vw, 5.2rem);
    font-weight: 900;
    line-height: 1.05;
    background: linear-gradient(135deg, #fff 20%, var(--cyan) 55%, var(--green) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    opacity: 0; animation: fadeUp .8s .4s forwards;
    filter: drop-shadow(0 0 30px rgba(0,201,255,.4));
  }

  .hero-sub {
    font-family: 'Space Mono', monospace;
    font-size: clamp(.85rem, 2vw, 1.08rem);
    color: rgba(205,237,245,.55);
    margin-top: 14px;
    opacity: 0; animation: fadeUp .8s .65s forwards;
  }

  /* Typing text */
  .typing-wrap {
    margin-top: 28px;
    font-family: 'Orbitron', monospace;
    font-size: clamp(.9rem, 2.2vw, 1.18rem);
    color: var(--cyan);
    letter-spacing: .06em;
    min-height: 2em;
    opacity: 0; animation: fadeUp .8s .85s forwards;
  }
  .typing-cursor {
    display: inline-block;
    width: 2px; height: 1.1em;
    background: var(--cyan);
    margin-left: 3px;
    vertical-align: middle;
    animation: blink 0.75s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* CGPA badge */
  .cgpa-badge {
    margin-top: 36px;
    display: inline-flex; align-items: center; gap: 10px;
    background: rgba(0,201,255,.08); border: 1px solid var(--border);
    border-radius: 50px; padding: 10px 24px;
    font-family: 'Space Mono', monospace; font-size: .88rem;
    opacity: 0; animation: fadeUp .8s 1.1s forwards;
    backdrop-filter: blur(10px);
  }
  .cgpa-dot { width: 10px; height: 10px; border-radius: 50%; background: var(--green); box-shadow: 0 0 10px var(--green); animation: pulse-dot 1.8s ease-in-out infinite; }
  @keyframes pulse-dot { 0%,100%{transform:scale(1); opacity:1} 50%{transform:scale(1.5); opacity:.6} }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 32px;
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    font-size: .7rem; letter-spacing: .15em; color: rgba(0,201,255,.4);
    text-transform: uppercase; font-family: 'Space Mono', monospace;
    animation: fadeIn 1s 2s both;
  }
  .scroll-line { width: 1px; height: 50px; background: linear-gradient(var(--cyan), transparent); animation: scrollPulse 2s ease-in-out infinite; }
  @keyframes scrollPulse { 0%,100%{opacity:.3; transform:scaleY(1)} 50%{opacity:1; transform:scaleY(1.3)} }

  /* ─── SECTION WRAPPER ─── */
  section { position: relative; z-index: 1; padding: 80px 24px; max-width: 1100px; margin: 0 auto; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: .7rem; letter-spacing: .3em; text-transform: uppercase;
    color: var(--cyan); margin-bottom: 12px;
    opacity: 0; transform: translateX(-20px);
    transition: opacity .6s, transform .6s;
  }
  .section-label.vis { opacity:1; transform:translateX(0); }

  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(1.5rem, 4vw, 2.3rem);
    font-weight: 700;
    color: #fff;
    margin-bottom: 48px;
    opacity: 0; transform: translateY(20px);
    transition: opacity .6s .1s, transform .6s .1s;
  }
  .section-title.vis { opacity:1; transform:translateY(0); }
  .section-title span { color: var(--cyan); }

  /* ─── DIVIDER ─── */
  .divider {
    width: 100%; height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    margin: 0 auto;
    position: relative; z-index: 1;
    opacity: 0; transition: opacity .8s;
  }
  .divider.vis { opacity:1; }

  /* ─── ABOUT GRID ─── */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  @media(max-width:640px){ .about-grid{ grid-template-columns:1fr; } }

  .about-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px 24px;
    position: relative; overflow: hidden;
    opacity: 0; transform: translateY(30px);
    transition: opacity .6s, transform .6s, border-color .3s, box-shadow .3s;
  }
  .about-card.vis { opacity:1; transform:translateY(0); }
  .about-card:hover { border-color: var(--cyan); box-shadow: 0 0 30px rgba(0,201,255,.15), inset 0 0 20px rgba(0,201,255,.04); }
  .about-card::after {
    content: '';
    position: absolute; top: -50%; left: -50%;
    width: 200%; height: 200%;
    background: conic-gradient(from 0deg at 50% 50%, transparent 0deg, rgba(0,201,255,.08) 60deg, transparent 120deg);
    animation: rotate 8s linear infinite;
    opacity: 0; transition: opacity .4s;
  }
  .about-card:hover::after { opacity: 1; }
  @keyframes rotate { to { transform: rotate(360deg); } }

  .about-card .icon { font-size: 2rem; margin-bottom: 12px; }
  .about-card h3 { font-family: 'Orbitron', monospace; font-size: .9rem; color: var(--cyan); margin-bottom: 8px; letter-spacing: .05em; }
  .about-card p { font-size: .93rem; color: rgba(205,237,245,.7); line-height: 1.7; }

  /* ─── SKILLS ─── */
  .skills-grid {
    display: flex; flex-wrap: wrap; gap: 14px;
  }
  .skill-chip {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 10px 18px;
    font-family: 'Space Mono', monospace;
    font-size: .78rem;
    color: rgba(205,237,245,.8);
    cursor: default;
    position: relative; overflow: hidden;
    opacity: 0; transform: scale(.9);
    transition: opacity .4s, transform .4s, border-color .3s, color .3s, box-shadow .3s;
  }
  .skill-chip.vis { opacity:1; transform:scale(1); }
  .skill-chip:hover {
    border-color: var(--cyan); color: var(--cyan);
    box-shadow: 0 0 20px rgba(0,201,255,.25);
    transform: scale(1.05) translateY(-2px);
  }
  .skill-chip::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,201,255,.08), transparent);
    opacity: 0; transition: opacity .3s;
  }
  .skill-chip:hover::before { opacity: 1; }

  /* ─── PROJECTS ─── */
  .projects-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 24px;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 32px 28px;
    position: relative; overflow: hidden;
    opacity: 0; transform: translateY(40px);
    transition: opacity .6s, transform .6s, border-color .3s, box-shadow .3s;
    cursor: pointer;
  }
  .project-card.vis { opacity:1; transform:translateY(0); }
  .project-card:hover { border-color: var(--cyan); box-shadow: 0 8px 50px rgba(0,201,255,.18); transform: translateY(-6px); }

  .project-icon {
    font-size: 2.4rem; margin-bottom: 18px;
    display: inline-block;
    animation: float 4s ease-in-out infinite;
  }
  @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-8px)} }

  .project-card h3 { font-family: 'Orbitron', monospace; font-size: 1rem; color: #fff; margin-bottom: 12px; line-height: 1.4; }
  .project-card p { font-size: .88rem; color: rgba(205,237,245,.6); line-height: 1.7; margin-bottom: 18px; }

  .tag-row { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag {
    background: rgba(0,201,255,.1); border: 1px solid rgba(0,201,255,.2);
    border-radius: 20px; padding: 4px 12px;
    font-size: .72rem; color: var(--cyan); font-family: 'Space Mono', monospace;
  }

  /* Project glow bar */
  .project-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--green));
    transform: scaleX(0); transform-origin: left;
    transition: transform .4s ease;
  }
  .project-card:hover::before { transform: scaleX(1); }

  /* ─── EXPERIENCE / TIMELINE ─── */
  .timeline { position: relative; padding-left: 32px; }
  .timeline::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0; width: 1px;
    background: linear-gradient(var(--cyan), var(--green), transparent);
  }
  .tl-item {
    position: relative; margin-bottom: 40px;
    opacity: 0; transform: translateX(-20px);
    transition: opacity .6s, transform .6s;
  }
  .tl-item.vis { opacity:1; transform:translateX(0); }
  .tl-dot {
    position: absolute; left: -38px; top: 4px;
    width: 13px; height: 13px; border-radius: 50%;
    background: var(--cyan);
    box-shadow: 0 0 16px var(--cyan);
    animation: pulse-dot 2s ease-in-out infinite;
  }
  .tl-date { font-family: 'Space Mono', monospace; font-size: .72rem; color: var(--green); margin-bottom: 6px; letter-spacing: .1em; }
  .tl-title { font-family: 'Orbitron', monospace; font-size: 1rem; color: #fff; margin-bottom: 6px; }
  .tl-sub { font-size: .88rem; color: rgba(205,237,245,.55); margin-bottom: 12px; }
  .tl-list { list-style: none; }
  .tl-list li { font-size: .88rem; color: rgba(205,237,245,.7); padding: 4px 0 4px 18px; position: relative; }
  .tl-list li::before { content: '▹'; position: absolute; left: 0; color: var(--cyan); }

  /* ─── STATS ─── */
  .stats-row {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 20px; margin-top: 8px;
  }
  .stat-box {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 28px 20px; text-align: center;
    opacity: 0; transform: scale(.9);
    transition: opacity .5s, transform .5s, border-color .3s, box-shadow .3s;
  }
  .stat-box.vis { opacity:1; transform:scale(1); }
  .stat-box:hover { border-color: var(--green); box-shadow: 0 0 30px rgba(146,254,157,.15); }
  .stat-num {
    font-family: 'Orbitron', monospace; font-size: 2.2rem; font-weight: 900;
    background: linear-gradient(135deg, var(--cyan), var(--green));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    display: block;
  }
  .stat-label { font-size: .78rem; color: rgba(205,237,245,.5); margin-top: 6px; font-family: 'Space Mono', monospace; }

  /* ─── CERTIFICATIONS ─── */
  .cert-list { display: flex; flex-direction: column; gap: 16px; }
  .cert-item {
    display: flex; align-items: center; gap: 18px;
    background: var(--card); border: 1px solid var(--border);
    border-radius: 14px; padding: 20px 24px;
    opacity: 0; transform: translateX(20px);
    transition: opacity .5s, transform .5s, border-color .3s;
  }
  .cert-item.vis { opacity:1; transform:translateX(0); }
  .cert-item:hover { border-color: var(--green); }
  .cert-icon { font-size: 1.6rem; flex-shrink: 0; }
  .cert-name { font-family: 'Space Mono', monospace; font-size: .9rem; color: #fff; }
  .cert-org { font-size: .8rem; color: rgba(205,237,245,.5); margin-top: 3px; }

  /* ─── CONNECT ─── */
  .connect-grid { display: flex; flex-wrap: wrap; gap: 16px; justify-content: center; margin-top: 8px; }
  .connect-btn {
    display: flex; align-items: center; gap: 10px;
    padding: 14px 28px;
    border: 1px solid var(--border); border-radius: 50px;
    background: var(--card); text-decoration: none;
    font-family: 'Space Mono', monospace; font-size: .85rem; color: rgba(205,237,245,.8);
    transition: all .3s; position: relative; overflow: hidden;
    opacity: 0; transform: translateY(20px);
  }
  .connect-btn.vis { opacity:1; transform:translateY(0); }
  .connect-btn::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,201,255,.12), rgba(146,254,157,.08));
    opacity: 0; transition: opacity .3s;
  }
  .connect-btn:hover { border-color: var(--cyan); color: var(--cyan); box-shadow: 0 0 25px rgba(0,201,255,.2); transform: translateY(-3px); }
  .connect-btn:hover::before { opacity:1; }

  /* ─── FOOTER ─── */
  footer {
    position: relative; z-index: 1;
    text-align: center; padding: 48px 24px;
    font-family: 'Space Mono', monospace; font-size: .78rem;
    color: rgba(205,237,245,.25);
    letter-spacing: .12em;
  }
  footer span { color: var(--cyan); }

  /* ─── ANIMATIONS ─── */
  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeIn { from{opacity:0} to{opacity:1} }

  /* ─── SCAN LINES OVERLAY ─── */
  body::after {
    content: '';
    position: fixed; inset: 0; z-index: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 3px, rgba(0,0,0,.06) 3px, rgba(0,0,0,.06) 4px);
    pointer-events: none;
  }

  /* ─── GLITCH EFFECT ON NAME ─── */
  .hero-name {
    position: relative;
  }
  .hero-name::before, .hero-name::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0; width: 100%;
    background: linear-gradient(135deg, #fff 20%, var(--cyan) 55%, var(--green) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .hero-name::before {
    animation: glitch1 4s infinite linear;
    clip-path: polygon(0 20%, 100% 20%, 100% 35%, 0 35%);
  }
  .hero-name::after {
    animation: glitch2 4s infinite linear;
    clip-path: polygon(0 60%, 100% 60%, 100% 75%, 0 75%);
  }
  @keyframes glitch1 {
    0%,90%,100% { transform: translate(0); opacity:0; }
    91% { transform: translate(-3px, 1px); opacity:.7; }
    93% { transform: translate(2px, -1px); opacity:.5; }
    95% { transform: translate(0); opacity:0; }
  }
  @keyframes glitch2 {
    0%,93%,100% { transform: translate(0); opacity:0; }
    94% { transform: translate(3px, -1px); opacity:.7; }
    96% { transform: translate(-2px, 1px); opacity:.5; }
    98% { transform: translate(0); opacity:0; }
  }

  /* Neon border animated */
  .neon-border {
    position: relative;
  }
  .neon-border::after {
    content: '';
    position: absolute; inset: -1px;
    border-radius: inherit;
    background: linear-gradient(90deg, var(--cyan), var(--green), var(--cyan));
    background-size: 200% 100%;
    animation: borderSlide 3s linear infinite;
    z-index: -1;
    opacity: .6;
  }
  @keyframes borderSlide { to { background-position: 200% 0; } }

  /* Hackathon badges */
  .hackathon-grid { display:flex; flex-wrap:wrap; gap:16px; }
  .hack-badge {
    background: linear-gradient(135deg, rgba(0,201,255,.08), rgba(146,254,157,.05));
    border: 1px solid var(--border); border-radius: 14px;
    padding: 22px 26px; flex: 1; min-width: 220px;
    opacity: 0; transform: scale(.92);
    transition: opacity .5s, transform .5s, box-shadow .3s;
  }
  .hack-badge.vis { opacity:1; transform:scale(1); }
  .hack-badge:hover { box-shadow: 0 0 30px rgba(0,201,255,.2); }
  .hack-badge .hb-title { font-family: 'Orbitron', monospace; font-size: .9rem; color: var(--cyan); margin-bottom: 6px; }
  .hack-badge .hb-sub { font-size: .82rem; color: rgba(205,237,245,.5); }

  /* Interests */
  .interests-wrap { display:flex; flex-wrap:wrap; gap:14px; }
  .interest-pill {
    display: flex; align-items: center; gap: 8px;
    background: var(--card); border: 1px solid var(--border);
    border-radius: 50px; padding: 10px 20px;
    font-size: .85rem; color: rgba(205,237,245,.8);
    opacity:0; transform:translateY(16px);
    transition: opacity .5s, transform .5s, border-color .3s, box-shadow .3s;
  }
  .interest-pill.vis { opacity:1; transform:translateY(0); }
  .interest-pill:hover { border-color: var(--green); box-shadow: 0 0 20px rgba(146,254,157,.15); }
  .interest-pill .i-icon { font-size:1.1rem; }

  /* Nav dots */
  #nav-dots {
    position: fixed; right: 24px; top: 50%; transform: translateY(-50%);
    z-index: 100; display: flex; flex-direction: column; gap: 12px;
  }
  .nav-dot {
    width: 8px; height: 8px; border-radius: 50%;
    border: 1px solid rgba(0,201,255,.4); cursor: pointer;
    transition: all .3s;
  }
  .nav-dot.active, .nav-dot:hover {
    background: var(--cyan);
    box-shadow: 0 0 12px var(--cyan);
    transform: scale(1.4);
  }

</style>
</head>
<body>

<!-- Cursor -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- Stars canvas -->
<canvas id="stars"></canvas>

<!-- Nav dots -->
<nav id="nav-dots">
  <div class="nav-dot active" data-target="hero" title="Home"></div>
  <div class="nav-dot" data-target="about" title="About"></div>
  <div class="nav-dot" data-target="skills" title="Skills"></div>
  <div class="nav-dot" data-target="projects" title="Projects"></div>
  <div class="nav-dot" data-target="experience" title="Experience"></div>
  <div class="nav-dot" data-target="connect" title="Connect"></div>
</nav>

<!-- ══════════ HERO ══════════ -->
<div class="hero" id="hero">
  <div class="hero-tag">✦ AI & Machine Learning ✦</div>
  <h1 class="hero-name" data-text="Batna Yamini">Batna Yamini</h1>
  <p class="hero-sub">NRI Institute of Technology, Vijayawada</p>
  <div class="typing-wrap">
    <span id="typed-text"></span><span class="typing-cursor"></span>
  </div>
  <div class="cgpa-badge">
    <div class="cgpa-dot"></div>
    <span>B.Tech AI&ML &nbsp;·&nbsp; CGPA <strong style="color:var(--cyan)">8.7</strong></span>
  </div>
  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</div>

<div class="divider" style="max-width:900px;margin:0 auto;"></div>

<!-- ══════════ ABOUT ══════════ -->
<section id="about">
  <div class="section-label">01 — Introduction</div>
  <div class="section-title">About <span>Me</span></div>
  <div class="about-grid">
    <div class="about-card">
      <div class="icon">🎓</div>
      <h3>Education</h3>
      <p>B.Tech in Artificial Intelligence &amp; Machine Learning at NRI Institute of Technology, Vijayawada. Currently in 2nd year (2023–Present).</p>
    </div>
    <div class="about-card">
      <div class="icon">💡</div>
      <h3>Passion</h3>
      <p>Motivated by the power of intelligent systems to solve real-world problems. Loves building AI-powered applications that make a tangible difference.</p>
    </div>
    <div class="about-card">
      <div class="icon">🚀</div>
      <h3>Goal</h3>
      <p>Aspiring AI researcher focused on developing cutting-edge ML solutions and contributing to the frontier of artificial intelligence research.</p>
    </div>
    <div class="about-card">
      <div class="icon">📊</div>
      <h3>Coursework</h3>
      <p>Data Structures &amp; Algorithms · Python Programming · Database Management Systems · Artificial Intelligence</p>
    </div>
  </div>

  <div class="stats-row" style="margin-top:40px;">
    <div class="stat-box"><span class="stat-num" data-target="8.7">0</span><div class="stat-label">CGPA</div></div>
    <div class="stat-box"><span class="stat-num" data-target="3">0</span><div class="stat-label">Projects</div></div>
    <div class="stat-box"><span class="stat-num" data-target="2">0</span><div class="stat-label">Hackathons</div></div>
    <div class="stat-box"><span class="stat-num" data-target="5">0</span><div class="stat-label">Tech Stacks</div></div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════ SKILLS ══════════ -->
<section id="skills">
  <div class="section-label">02 — Arsenal</div>
  <div class="section-title">Technical <span>Skills</span></div>

  <p style="font-family:'Space Mono',monospace;font-size:.78rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase;margin-bottom:16px;">Programming Languages</p>
  <div class="skills-grid" id="langs-grid"></div>

  <p style="font-family:'Space Mono',monospace;font-size:.78rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase;margin:36px 0 16px;">Frameworks & Libraries</p>
  <div class="skills-grid" id="fw-grid"></div>

  <p style="font-family:'Space Mono',monospace;font-size:.78rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase;margin:36px 0 16px;">AI Tools</p>
  <div class="skills-grid" id="ai-grid"></div>

  <div style="margin-top:48px;">
    <p style="font-family:'Space Mono',monospace;font-size:.78rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase;margin-bottom:20px;">Research Interests</p>
    <div class="interests-wrap" id="interests-wrap"></div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════ PROJECTS ══════════ -->
<section id="projects">
  <div class="section-label">03 — Work</div>
  <div class="section-title">Featured <span>Projects</span></div>
  <div class="projects-grid">
    <div class="project-card neon-border">
      <span class="project-icon">🩺</span>
      <h3>AI-Based Multi-Disease Prediction System</h3>
      <p>Predicts Diabetes, Heart Disease &amp; Parkinson's Disease using 40+ clinical features with real-time ML inference through an interactive Streamlit UI.</p>
      <div class="tag-row">
        <span class="tag">Python</span><span class="tag">Streamlit</span><span class="tag">Scikit-learn</span><span class="tag">Healthcare AI</span>
      </div>
    </div>
    <div class="project-card">
      <span class="project-icon" style="animation-delay:.8s">♟</span>
      <h3>ML-Powered Chess Engine with Django</h3>
      <p>Chess engine combining Minimax + Alpha-Beta Pruning with a Random Forest model for board evaluation. Feature-based board representation with a web-based interactive interface.</p>
      <div class="tag-row">
        <span class="tag">Python</span><span class="tag">Django</span><span class="tag">Scikit-learn</span><span class="tag">Game AI</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════ EXPERIENCE ══════════ -->
<section id="experience">
  <div class="section-label">04 — Journey</div>
  <div class="section-title">Experience &amp; <span>Achievements</span></div>

  <div class="timeline">
    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-date">2025</div>
      <div class="tl-title">AI Transformative Learning Intern</div>
      <div class="tl-sub">TechSaksham</div>
      <ul class="tl-list">
        <li>Developed a multi-disease prediction ML web application</li>
        <li>Integrated multiple pretrained models into a unified system</li>
        <li>Built interactive UI using Streamlit for real-time predictions</li>
        <li>Enabled healthcare predictions for Diabetes, Heart Disease &amp; Parkinson's</li>
      </ul>
    </div>
    <div class="tl-item">
      <div class="tl-dot" style="background:var(--green);box-shadow:0 0 16px var(--green)"></div>
      <div class="tl-date">2024–2025</div>
      <div class="tl-title">Hackathon Participant</div>
      <div class="tl-sub">RGUKT IIIT Nuzvid &amp; PB Siddhartha College</div>
      <ul class="tl-list">
        <li>AI Agents Hackathon — RGUKT IIIT Nuzvid</li>
        <li>AIgnite Hackathon — PB Siddhartha College</li>
      </ul>
    </div>
    <div class="tl-item">
      <div class="tl-dot" style="background:#fff;box-shadow:0 0 16px #fff"></div>
      <div class="tl-date">2023 — Present</div>
      <div class="tl-title">B.Tech — AI & Machine Learning</div>
      <div class="tl-sub">NRI Institute of Technology, Vijayawada &nbsp;·&nbsp; CGPA 8.7</div>
    </div>
  </div>

  <div style="margin-top:48px;">
    <p style="font-family:'Space Mono',monospace;font-size:.78rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase;margin-bottom:20px;">Certifications</p>
    <div class="cert-list">
      <div class="cert-item">
        <span class="cert-icon">📜</span>
        <div>
          <div class="cert-name">TechSaksham AI Internship Certificate</div>
          <div class="cert-org">Microsoft &amp; SAP — TechSaksham Program</div>
        </div>
      </div>
      <div class="cert-item">
        <span class="cert-icon">🐍</span>
        <div>
          <div class="cert-name">Python Programming Certification</div>
          <div class="cert-org">GeeksforGeeks</div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════ CONNECT ══════════ -->
<section id="connect" style="text-align:center;">
  <div class="section-label" style="text-align:center;transform:none;">05 — Reach Out</div>
  <div class="section-title" style="text-align:center;">Let's <span>Connect</span></div>
  <p style="max-width:520px;margin:0 auto 40px;color:rgba(205,237,245,.55);font-size:.95rem;line-height:1.8;">
    Open to collaborations, research discussions, AI projects, and new opportunities. Feel free to reach out!
  </p>
  <div class="connect-grid">
    <a href="https://linkedin.com/in/YOUR_LINKEDIN" class="connect-btn">
      <span>💼</span> LinkedIn
    </a>
    <a href="mailto:yaminibatna@gmail.com" class="connect-btn">
      <span>📧</span> yaminibatna@gmail.com
    </a>
    <a href="https://github.com/YOUR_GITHUB_USERNAME" class="connect-btn">
      <span>🐙</span> GitHub
    </a>
  </div>

  <p style="margin-top:60px;font-family:'Orbitron',monospace;font-size:.9rem;color:rgba(205,237,245,.25);letter-spacing:.08em;">
    ✦ Building AI solutions today for a smarter tomorrow. ✦
  </p>
</section>

<footer>
  <span>Batna Yamini</span> &nbsp;·&nbsp; AI & Machine Learning &nbsp;·&nbsp; Vijayawada, India<br/>
  <span style="color:rgba(205,237,245,.15);font-size:.65rem;margin-top:8px;display:block;">Crafted with 💙 &amp; Orbitron</span>
</footer>

<script>
// ─── CURSOR ───
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove', e=>{
  mx=e.clientX; my=e.clientY;
  cursor.style.left=mx+'px'; cursor.style.top=my+'px';
});
(function animRing(){
  rx += (mx-rx)*.12; ry += (my-ry)*.12;
  ring.style.left=rx+'px'; ring.style.top=ry+'px';
  requestAnimationFrame(animRing);
})();
document.querySelectorAll('a,button,.about-card,.project-card,.skill-chip,.connect-btn').forEach(el=>{
  el.addEventListener('mouseenter',()=>{ cursor.style.width='22px'; cursor.style.height='22px'; ring.style.width='60px'; ring.style.height='60px'; });
  el.addEventListener('mouseleave',()=>{ cursor.style.width='14px'; cursor.style.height='14px'; ring.style.width='40px'; ring.style.height='40px'; });
});

// ─── STARS ───
const canvas = document.getElementById('stars');
const ctx = canvas.getContext('2d');
let W,H,stars=[];
function resizeCanvas(){ W=canvas.width=window.innerWidth; H=canvas.height=window.innerHeight; }
function initStars(){
  stars=[];
  for(let i=0;i<220;i++) stars.push({
    x:Math.random()*W, y:Math.random()*H,
    r:Math.random()*1.4+.2,
    speed:Math.random()*.3+.05,
    twinkle:Math.random()*Math.PI*2
  });
}
function drawStars(t){
  ctx.clearRect(0,0,W,H);
  stars.forEach(s=>{
    s.twinkle+=.015;
    const a=.25+.5*Math.abs(Math.sin(s.twinkle));
    ctx.beginPath();
    ctx.arc(s.x,s.y,s.r,0,Math.PI*2);
    ctx.fillStyle=`rgba(0,201,255,${a})`;
    ctx.fill();
    s.y+=s.speed;
    if(s.y>H){ s.y=-4; s.x=Math.random()*W; }
  });
  requestAnimationFrame(drawStars);
}
resizeCanvas(); initStars(); drawStars();
window.addEventListener('resize',()=>{ resizeCanvas(); initStars(); });

// ─── TYPING ───
const phrases = [
  'AI & Machine Learning Student',
  'Future AI Researcher',
  'Building Intelligent Systems',
  'ML-Powered App Developer',
  'Passionate Problem Solver'
];
let pi=0,ci=0,deleting=false,pause=0;
const typedEl = document.getElementById('typed-text');
function type(){
  const cur=phrases[pi];
  if(pause>0){ pause--; setTimeout(type,50); return; }
  if(!deleting){
    typedEl.textContent=cur.slice(0,++ci);
    if(ci===cur.length){ deleting=true; pause=50; }
    setTimeout(type,72);
  } else {
    typedEl.textContent=cur.slice(0,--ci);
    if(ci===0){ deleting=false; pi=(pi+1)%phrases.length; pause=12; }
    setTimeout(type,36);
  }
}
type();

// ─── POPULATE SKILLS ───
const langSkills = ['Python','C','JavaScript','HTML','CSS','SQL'];
const fwSkills = ['React','Node.js','Flask','Pandas','NumPy','Scikit-Learn'];
const aiSkills = ['OpenAI API','GPT Models','Google Gemini API','Perplexity AI'];
const interests = ['🧠 Machine Learning','🤖 AI Applications','📊 Decision Support Systems','🌐 AI-powered Web Apps'];

function fillGrid(id, items){
  const g=document.getElementById(id);
  items.forEach((s,i)=>{
    const c=document.createElement('div');
    c.className='skill-chip';
    c.textContent=s;
    c.style.transitionDelay=(i*.07)+'s';
    g.appendChild(c);
  });
}
fillGrid('langs-grid',langSkills);
fillGrid('fw-grid',fwSkills);
fillGrid('ai-grid',aiSkills);

const iw=document.getElementById('interests-wrap');
interests.forEach((t,i)=>{
  const d=document.createElement('div');
  d.className='interest-pill';
  d.innerHTML=`<span class="i-icon">${t.slice(0,2)}</span> ${t.slice(3)}`;
  d.style.transitionDelay=(i*.1)+'s';
  iw.appendChild(d);
});

// ─── INTERSECTION OBSERVER ───
const observer = new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.classList.add('vis');
    }
  });
},{threshold:.12});

document.querySelectorAll('.about-card,.stat-box,.project-card,.tl-item,.cert-item,.skill-chip,.interest-pill,.connect-btn,.hack-badge,.section-label,.section-title,.divider').forEach(el=>observer.observe(el));

// ─── COUNTER ANIMATION ───
const numObserver = new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      const el=e.target;
      const target=parseFloat(el.dataset.target);
      const duration=1400;
      const start=performance.now();
      function tick(now){
        const t=Math.min((now-start)/duration,1);
        const eased=1-Math.pow(1-t,3);
        const val=eased*target;
        el.textContent=target%1!==0?val.toFixed(1):Math.round(val);
        if(t<1) requestAnimationFrame(tick);
        else el.textContent=target%1!==0?target.toFixed(1):target;
      }
      requestAnimationFrame(tick);
      numObserver.unobserve(el);
    }
  });
},{threshold:.5});
document.querySelectorAll('[data-target]').forEach(el=>numObserver.observe(el));

// ─── NAV DOTS ───
const sections=['hero','about','skills','projects','experience','connect'];
const dots=document.querySelectorAll('.nav-dot');
function updateDots(){
  let cur=0;
  sections.forEach((id,i)=>{
    const el=document.getElementById(id);
    if(el && el.getBoundingClientRect().top<=window.innerHeight/2) cur=i;
  });
  dots.forEach((d,i)=>d.classList.toggle('active',i===cur));
}
window.addEventListener('scroll',updateDots);
dots.forEach((d,i)=>{
  d.addEventListener('click',()=>{
    document.getElementById(sections[i])?.scrollIntoView({behavior:'smooth'});
  });
});

</script>
</body>
</html>
