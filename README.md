<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Prsanjeet Panwar — Developer Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #030712;
  --surface: #0d1117;
  --surface2: #161b22;
  --border: rgba(255,255,255,0.07);
  --accent: #00d9ff;
  --accent2: #7c3aed;
  --accent3: #f59e0b;
  --text: #e6edf3;
  --muted: #8b949e;
  --glow: 0 0 40px rgba(0,217,255,0.15);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'JetBrains Mono', monospace;
  min-height: 100vh;
  overflow-x: hidden;
  cursor: none;
}

/* ── Custom cursor ── */
#cursor {
  position: fixed; top: 0; left: 0; z-index: 9999;
  pointer-events: none;
  width: 12px; height: 12px;
  background: var(--accent);
  border-radius: 50%;
  transform: translate(-50%,-50%);
  transition: transform .1s, background .2s;
  mix-blend-mode: screen;
}
#cursor-ring {
  position: fixed; top: 0; left: 0; z-index: 9998;
  pointer-events: none;
  width: 36px; height: 36px;
  border: 1px solid rgba(0,217,255,.4);
  border-radius: 50%;
  transform: translate(-50%,-50%);
  transition: transform .25s ease, width .25s, height .25s, border-color .25s;
}
body:has(a:hover) #cursor-ring { width: 56px; height: 56px; border-color: var(--accent); }

/* ── Canvas grid bg ── */
#grid-canvas {
  position: fixed; inset: 0; z-index: 0; opacity: .35;
  pointer-events: none;
}

/* ── Floating particles ── */
.particles { position: fixed; inset: 0; z-index: 0; pointer-events: none; overflow: hidden; }
.particle {
  position: absolute;
  width: 2px; height: 2px;
  background: var(--accent);
  border-radius: 50%;
  animation: float-up linear infinite;
  opacity: 0;
}
@keyframes float-up {
  0%   { transform: translateY(100vh) translateX(0); opacity: 0; }
  10%  { opacity: 1; }
  90%  { opacity: .6; }
  100% { transform: translateY(-10vh) translateX(var(--dx,20px)); opacity: 0; }
}

/* ── Main layout ── */
.container {
  position: relative; z-index: 1;
  max-width: 900px;
  margin: 0 auto;
  padding: 0 24px 120px;
}

/* ── Hero ── */
.hero {
  padding: 100px 0 60px;
  display: flex; flex-direction: column; gap: 8px;
}

.hero-badge {
  display: inline-flex; align-items: center; gap: 8px;
  border: 1px solid var(--border);
  background: var(--surface2);
  padding: 6px 14px; border-radius: 100px;
  font-size: 11px; color: var(--muted); width: fit-content;
  animation: fade-up .6s ease both;
}
.hero-badge .dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: #22c55e;
  animation: pulse-dot 2s ease infinite;
}
@keyframes pulse-dot {
  0%,100% { box-shadow: 0 0 0 0 rgba(34,197,94,.4); }
  50%      { box-shadow: 0 0 0 6px rgba(34,197,94,0); }
}

.hero-name {
  font-family: 'Syne', sans-serif;
  font-size: clamp(3rem, 8vw, 6rem);
  font-weight: 800;
  line-height: .95;
  letter-spacing: -2px;
  animation: fade-up .7s .1s ease both;
  background: linear-gradient(135deg, #fff 0%, var(--accent) 60%, var(--accent2) 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-role {
  font-family: 'Syne', sans-serif;
  font-size: clamp(1rem, 2.5vw, 1.3rem);
  font-weight: 600;
  color: var(--muted);
  animation: fade-up .7s .2s ease both;
  letter-spacing: .5px;
}

.hero-desc {
  font-size: 13px;
  line-height: 1.8;
  color: var(--muted);
  max-width: 560px;
  animation: fade-up .7s .3s ease both;
}

.hero-cta {
  display: flex; gap: 12px; margin-top: 12px;
  animation: fade-up .7s .4s ease both;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 10px 22px; border-radius: 8px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 12px; font-weight: 500;
  text-decoration: none; border: none; cursor: none;
  transition: transform .2s, box-shadow .2s, background .2s;
  position: relative; overflow: hidden;
}
.btn::before {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(255,255,255,.1), transparent);
  opacity: 0; transition: opacity .2s;
}
.btn:hover::before { opacity: 1; }
.btn:hover { transform: translateY(-2px); }

.btn-primary {
  background: var(--accent); color: #000; font-weight: 600;
}
.btn-primary:hover { box-shadow: 0 8px 32px rgba(0,217,255,.4); }

.btn-ghost {
  background: var(--surface2); color: var(--text);
  border: 1px solid var(--border);
}
.btn-ghost:hover { border-color: var(--accent); box-shadow: 0 0 0 1px var(--accent); }

@keyframes fade-up {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── Typing animation ── */
.typing-text {
  color: var(--accent);
  font-family: 'JetBrains Mono', monospace;
}
.typing-cursor { animation: blink .7s step-end infinite; }
@keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0; } }

/* ── Section headers ── */
.section { margin-top: 80px; }

.section-label {
  display: flex; align-items: center; gap: 12px;
  margin-bottom: 28px;
}
.section-label span {
  font-family: 'Syne', sans-serif;
  font-size: 1.2rem; font-weight: 700;
  letter-spacing: -.5px;
}
.section-label::before {
  content: ''; flex: none;
  width: 4px; height: 20px; border-radius: 2px;
  background: linear-gradient(to bottom, var(--accent), var(--accent2));
}
.section-label::after {
  content: ''; flex: 1;
  height: 1px; background: var(--border);
}

/* ── Project cards ── */
.projects-grid { display: grid; gap: 16px; }

.project-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 28px;
  position: relative; overflow: hidden;
  transition: border-color .3s, transform .3s, box-shadow .3s;
  cursor: none;
}
.project-card::before {
  content: '';
  position: absolute; inset: 0;
  background: radial-gradient(600px circle at var(--mx,50%) var(--my,50%), rgba(0,217,255,.06), transparent 40%);
  opacity: 0; transition: opacity .3s;
}
.project-card:hover::before { opacity: 1; }
.project-card:hover {
  border-color: rgba(0,217,255,.3);
  transform: translateY(-4px);
  box-shadow: 0 20px 60px rgba(0,0,0,.4), 0 0 0 1px rgba(0,217,255,.1);
}

.project-number {
  font-size: 10px; color: var(--accent); letter-spacing: 2px;
  text-transform: uppercase; margin-bottom: 10px;
}
.project-title {
  font-family: 'Syne', sans-serif;
  font-size: 1.3rem; font-weight: 700;
  margin-bottom: 10px; letter-spacing: -.5px;
  display: flex; align-items: center; gap: 10px;
}
.project-title .icon {
  width: 32px; height: 32px;
  background: var(--surface2);
  border-radius: 8px; border: 1px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  font-size: 16px;
}
.project-desc {
  font-size: 12px; line-height: 1.8; color: var(--muted); margin-bottom: 18px;
}
.tech-tags { display: flex; flex-wrap: wrap; gap: 6px; }
.tag {
  font-size: 10px; padding: 4px 10px; border-radius: 100px;
  background: var(--surface2); border: 1px solid var(--border);
  color: var(--muted); letter-spacing: .5px; font-weight: 500;
  transition: border-color .2s, color .2s;
}
.project-card:hover .tag { border-color: rgba(0,217,255,.2); color: var(--text); }

/* ── Tech stack ── */
.stack-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 12px;
}
.stack-group {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 12px; padding: 18px;
  transition: border-color .3s, transform .2s;
  cursor: none;
}
.stack-group:hover {
  border-color: rgba(0,217,255,.25);
  transform: translateY(-2px);
}
.stack-group-label {
  font-size: 10px; color: var(--accent); letter-spacing: 2px;
  text-transform: uppercase; margin-bottom: 12px; font-weight: 600;
}
.stack-items { display: flex; flex-wrap: wrap; gap: 6px; }
.stack-item {
  font-size: 11px; padding: 4px 10px;
  background: var(--surface2); border: 1px solid var(--border);
  border-radius: 6px; color: var(--text);
  transition: background .2s, border-color .2s, transform .15s;
}
.stack-item:hover {
  background: rgba(0,217,255,.1);
  border-color: rgba(0,217,255,.3);
  transform: scale(1.05);
}

/* ── Experience timeline ── */
.timeline { display: flex; flex-direction: column; gap: 0; }
.timeline-item {
  display: grid; grid-template-columns: 1px 1fr;
  gap: 0 24px;
  padding-bottom: 36px;
  position: relative;
  opacity: 0; transform: translateX(-20px);
  transition: opacity .5s, transform .5s;
}
.timeline-item.visible { opacity: 1; transform: translateX(0); }
.timeline-line {
  background: linear-gradient(to bottom, var(--accent), var(--accent2));
  border-radius: 2px;
  position: relative;
}
.timeline-dot {
  position: absolute; top: 4px; left: 50%;
  transform: translateX(-50%);
  width: 10px; height: 10px;
  background: var(--accent); border-radius: 50%;
  border: 2px solid var(--bg);
  box-shadow: 0 0 0 3px rgba(0,217,255,.2), 0 0 12px var(--accent);
}
.timeline-content {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 12px; padding: 20px;
}
.timeline-role {
  font-family: 'Syne', sans-serif;
  font-size: 1rem; font-weight: 700; margin-bottom: 4px;
}
.timeline-company {
  font-size: 11px; color: var(--accent); margin-bottom: 4px; font-weight: 500;
}
.timeline-period {
  font-size: 10px; color: var(--muted); margin-bottom: 10px; letter-spacing: .5px;
}
.timeline-desc { font-size: 11px; color: var(--muted); line-height: 1.7; }

/* ── Achievements ── */
.achievements { display: grid; gap: 10px; }
.achievement {
  display: flex; align-items: center; gap: 16px;
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 12px; padding: 16px 20px;
  transition: border-color .3s, transform .2s;
  opacity: 0; transform: translateY(16px);
  transition: opacity .4s, transform .4s, border-color .3s;
  cursor: none;
}
.achievement.visible { opacity: 1; transform: translateY(0); }
.achievement:hover { border-color: rgba(245,158,11,.3); transform: translateX(4px); }
.achievement-medal { font-size: 24px; flex: none; filter: drop-shadow(0 0 8px rgba(245,158,11,.5)); }
.achievement-text { font-size: 12px; line-height: 1.6; }
.achievement-text strong { font-family: 'Syne', sans-serif; font-weight: 700; display: block; margin-bottom: 2px; }
.achievement-text span { color: var(--muted); font-size: 11px; }

/* ── Connect ── */
.connect-grid { display: flex; gap: 12px; flex-wrap: wrap; }
.connect-link {
  display: inline-flex; align-items: center; gap: 10px;
  background: var(--surface); border: 1px solid var(--border);
  padding: 12px 20px; border-radius: 10px;
  text-decoration: none; color: var(--text);
  font-size: 12px; transition: all .3s; cursor: none;
}
.connect-link:hover {
  border-color: var(--accent);
  background: rgba(0,217,255,.05);
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(0,0,0,.3);
}
.connect-link svg { flex: none; }

/* ── Footer ── */
.footer {
  margin-top: 80px;
  padding-top: 32px;
  border-top: 1px solid var(--border);
  display: flex; justify-content: space-between; align-items: center;
  flex-wrap: wrap; gap: 12px;
}
.footer-text { font-size: 11px; color: var(--muted); }
.footer-text span { color: var(--accent); }

/* ── Counter animation ── */
.stat-counter {
  font-family: 'Syne', sans-serif;
  font-size: 2rem; font-weight: 800;
  color: var(--accent);
}

.stats-row {
  display: grid; grid-template-columns: repeat(3, 1fr);
  gap: 12px; margin-top: 24px;
}
.stat-box {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 12px; padding: 20px;
  text-align: center;
  transition: border-color .3s;
}
.stat-box:hover { border-color: rgba(0,217,255,.3); }
.stat-label { font-size: 10px; color: var(--muted); margin-top: 6px; letter-spacing: 1px; text-transform: uppercase; }

/* ── Glowing divider ── */
.glow-divider {
  height: 1px;
  background: linear-gradient(to right, transparent, var(--accent), transparent);
  margin: 16px 0;
  opacity: .4;
}

/* ── Reveal animations ── */
.reveal {
  opacity: 0; transform: translateY(20px);
  transition: opacity .6s ease, transform .6s ease;
}
.reveal.visible { opacity: 1; transform: translateY(0); }

/* ── Scrollbar ── */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--accent2); border-radius: 2px; }

/* ── Nav ── */
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 16px 24px;
  display: flex; justify-content: space-between; align-items: center;
  background: rgba(3,7,18,.8);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  animation: slide-down .5s ease both;
}
@keyframes slide-down {
  from { opacity: 0; transform: translateY(-100%); }
  to   { opacity: 1; transform: translateY(0); }
}
.nav-logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800; font-size: .95rem; letter-spacing: -.5px;
}
.nav-logo span { color: var(--accent); }
.nav-links { display: flex; gap: 24px; }
.nav-links a {
  text-decoration: none; color: var(--muted);
  font-size: 11px; letter-spacing: 1px;
  text-transform: uppercase;
  transition: color .2s; cursor: none;
}
.nav-links a:hover { color: var(--text); }

/* ── Code rain effect label ── */
.code-accent {
  color: var(--accent); font-size: 11px; letter-spacing: 1px;
}
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>
<canvas id="grid-canvas"></canvas>
<div class="particles" id="particles"></div>

<nav class="nav">
  <div class="nav-logo">P<span>.</span>Panwar</div>
  <div class="nav-links">
    <a href="#projects">Projects</a>
    <a href="#stack">Stack</a>
    <a href="#experience">Experience</a>
    <a href="#connect">Connect</a>
  </div>
</nav>

<div class="container">

  <!-- HERO -->
  <section class="hero">
    <div class="hero-badge">
      <span class="dot"></span>
      Open to full-stack & AI engineering roles
    </div>
    <h1 class="hero-name">Prsanjeet<br>Panwar</h1>
    <div class="hero-role">
      <span class="typing-text" id="typing"></span><span class="typing-cursor">_</span>
    </div>
    <p class="hero-desc">
      Full-Stack Developer from Udaipur, Rajasthan.<br>
      I build production-grade web apps and AI-powered tools that actually ship.
    </p>
    <div class="hero-cta">
      <a href="mailto:prsanjeetpanwar729@gmail.com" class="btn btn-primary">↗ Hire me</a>
      <a href="https://linkedin.com/in/prsanjeetpanwar" class="btn btn-ghost">LinkedIn ↗</a>
    </div>

    <div class="stats-row reveal">
      <div class="stat-box">
        <div class="stat-counter" data-target="2">0</div>
        <div class="stat-label">Featured Projects</div>
      </div>
      <div class="stat-box">
        <div class="stat-counter" data-target="3">0</div>
        <div class="stat-label">Hackathon Wins</div>
      </div>
      <div class="stat-box">
        <div class="stat-counter" data-target="1">0</div>
        <div class="stat-label">Patent</div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section class="section reveal" id="projects">
    <div class="section-label"><span>Featured Projects</span></div>
    <div class="projects-grid">

      <div class="project-card" data-card>
        <div class="project-number">01 / PROJECT</div>
        <div class="project-title">
          <div class="icon">🤖</div>
          AI Code Analyser
        </div>
        <p class="project-desc">
          Analyse any GitHub repo using AI. Get instant commit summaries, ask questions about any codebase in plain English, and visualise team contribution patterns with rich dashboards.
        </p>
        <div class="tech-tags">
          <span class="tag">Next.js</span>
          <span class="tag">TypeScript</span>
          <span class="tag">LangChain</span>
          <span class="tag">Gemini API</span>
          <span class="tag">pgvector</span>
          <span class="tag">Docker</span>
          <span class="tag">PostgreSQL</span>
        </div>
      </div>

      <div class="project-card" data-card>
        <div class="project-number">02 / PROJECT</div>
        <div class="project-title">
          <div class="icon">💻</div>
          Collaborative Code Editor
        </div>
        <p class="project-desc">
          Real-time multi-user IDE with live cursor sync, in-browser code execution, Stripe subscriptions and OAuth authentication. Monaco Editor with presence awareness.
        </p>
        <div class="tech-tags">
          <span class="tag">Next.js</span>
          <span class="tag">TypeScript</span>
          <span class="tag">Convex</span>
          <span class="tag">Clerk</span>
          <span class="tag">Stripe</span>
          <span class="tag">Monaco Editor</span>
          <span class="tag">PostgreSQL</span>
        </div>
      </div>

    </div>
  </section>

  <!-- STACK -->
  <section class="section reveal" id="stack">
    <div class="section-label"><span>Tech Stack</span></div>
    <div class="stack-grid">
      <div class="stack-group">
        <div class="stack-group-label">Frontend</div>
        <div class="stack-items">
          <span class="stack-item">React.js</span>
          <span class="stack-item">Next.js</span>
          <span class="stack-item">TypeScript</span>
          <span class="stack-item">Tailwind</span>
          <span class="stack-item">Shadcn UI</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-label">Backend</div>
        <div class="stack-items">
          <span class="stack-item">Node.js</span>
          <span class="stack-item">NestJS</span>
          <span class="stack-item">Fastify</span>
          <span class="stack-item">Express</span>
          <span class="stack-item">WebSockets</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-label">Databases</div>
        <div class="stack-items">
          <span class="stack-item">PostgreSQL</span>
          <span class="stack-item">MongoDB</span>
          <span class="stack-item">Redis</span>
          <span class="stack-item">Prisma ORM</span>
          <span class="stack-item">pgvector</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-label">Cloud & DevOps</div>
        <div class="stack-items">
          <span class="stack-item">AWS S3</span>
          <span class="stack-item">Azure</span>
          <span class="stack-item">Docker</span>
          <span class="stack-item">Kubernetes</span>
          <span class="stack-item">Vercel</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-label">AI & ML</div>
        <div class="stack-items">
          <span class="stack-item">LangChain</span>
          <span class="stack-item">Gemini API</span>
          <span class="stack-item">Vector DBs</span>
          <span class="stack-item">Embeddings</span>
        </div>
      </div>
    </div>
  </section>

  <!-- EXPERIENCE -->
  <section class="section" id="experience">
    <div class="section-label reveal"><span>Experience</span></div>
    <div class="timeline">
      <div class="timeline-item">
        <div class="timeline-line"><div class="timeline-dot"></div></div>
        <div class="timeline-content">
          <div class="timeline-role">Full-Stack Developer</div>
          <div class="timeline-company">@ ZeddLabz</div>
          <div class="timeline-period">Dec 2023 – Apr 2025</div>
          <div class="timeline-desc">Built financial analytics dashboard · Redis caching · AWS S3 pipeline · PostgreSQL optimization for high-throughput data workloads.</div>
        </div>
      </div>
      <div class="timeline-item">
        <div class="timeline-line"><div class="timeline-dot"></div></div>
        <div class="timeline-content">
          <div class="timeline-role">Web Dev Intern</div>
          <div class="timeline-company">@ Hoicko Technology</div>
          <div class="timeline-period">Apr 2023 – Jul 2023</div>
          <div class="timeline-desc">Built React applications · Designed reusable component libraries · REST API integration for production-grade consumer products.</div>
        </div>
      </div>
    </div>
  </section>

  <!-- ACHIEVEMENTS -->
  <section class="section reveal" id="achievements">
    <div class="section-label"><span>Achievements</span></div>
    <div class="achievements">
      <div class="achievement">
        <div class="achievement-medal">🥉</div>
        <div class="achievement-text">
          <strong>3rd Place — Smart India Hackathon</strong>
          <span>National Finals · Government of India</span>
        </div>
      </div>
      <div class="achievement">
        <div class="achievement-medal">🏅</div>
        <div class="achievement-text">
          <strong>National Finalist — Manthan Hackathon 2021</strong>
          <span>Top 115 of 2,200+ competing teams</span>
        </div>
      </div>
      <div class="achievement">
        <div class="achievement-medal">📜</div>
        <div class="achievement-text">
          <strong>Patent Co-Inventor</strong>
          <span>Fire Extinguishing Drone — autonomous aerial firefighting system</span>
        </div>
      </div>
    </div>
  </section>

  <!-- CONNECT -->
  <section class="section reveal" id="connect">
    <div class="section-label"><span>Let's Connect</span></div>
    <p style="font-size:12px; color:var(--muted); margin-bottom:20px; line-height:1.8;">
      Open to full-stack, AI engineering, and remote roles. Let's build something great.
    </p>
    <div class="connect-grid">
      <a href="https://linkedin.com/in/prsanjeetpanwar" class="connect-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="var(--accent)">
          <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
          <rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/>
        </svg>
        LinkedIn ↗
      </a>
      <a href="mailto:prsanjeetpanwar729@gmail.com" class="connect-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--accent)" stroke-width="2">
          <rect x="2" y="4" width="20" height="16" rx="2"/>
          <path d="m22 7-10 7L2 7"/>
        </svg>
        prsanjeetpanwar729@gmail.com
      </a>
      <a href="https://github.com/prsanjeetpanwar" class="connect-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="var(--accent)">
          <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
        </svg>
        GitHub ↗
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer reveal">
    <div class="footer-text">Built with <span>♥</span> — Prsanjeet Panwar © 2025</div>
    <div class="footer-text"><span>//</span> Udaipur, Rajasthan</div>
  </footer>

</div>

<script>
// ── Custom cursor
const cursor = document.getElementById('cursor');
const cursorRing = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
function animateCursor() {
  cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
  rx += (mx - rx) * .12; ry += (my - ry) * .12;
  cursorRing.style.left = rx + 'px'; cursorRing.style.top = ry + 'px';
  requestAnimationFrame(animateCursor);
}
animateCursor();

// ── Grid canvas
const canvas = document.getElementById('grid-canvas');
const ctx = canvas.getContext('2d');
function resizeCanvas() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
resizeCanvas(); window.addEventListener('resize', resizeCanvas);
function drawGrid() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  const size = 48;
  ctx.strokeStyle = 'rgba(0,217,255,0.06)';
  ctx.lineWidth = 1;
  for (let x = 0; x < canvas.width; x += size) {
    ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, canvas.height); ctx.stroke();
  }
  for (let y = 0; y < canvas.height; y += size) {
    ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(canvas.width, y); ctx.stroke();
  }
}
drawGrid();

// ── Particles
const pContainer = document.getElementById('particles');
function createParticle() {
  const p = document.createElement('div');
  p.className = 'particle';
  p.style.cssText = `
    left:${Math.random()*100}%;
    animation-duration:${5+Math.random()*8}s;
    animation-delay:${Math.random()*6}s;
    --dx:${(Math.random()-.5)*60}px;
    width:${Math.random()<.3?3:2}px;
    height:${Math.random()<.3?3:2}px;
    opacity:.8;
    background:${Math.random()<.2?'#7c3aed':'#00d9ff'};
  `;
  pContainer.appendChild(p);
}
for (let i = 0; i < 35; i++) createParticle();

// ── Typing animation
const phrases = ['Full-Stack Developer', 'AI Engineer', 'Next.js Specialist', 'Open Source Builder'];
let pi = 0, ci = 0, deleting = false;
const typingEl = document.getElementById('typing');
function type() {
  const phrase = phrases[pi];
  if (!deleting) {
    typingEl.textContent = phrase.slice(0, ++ci);
    if (ci === phrase.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    typingEl.textContent = phrase.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; }
  }
  setTimeout(type, deleting ? 40 : 80);
}
type();

// ── Scroll reveal
const revealEls = document.querySelectorAll('.reveal, .timeline-item, .achievement');
const io = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 60);
    }
  });
}, { threshold: .1 });
revealEls.forEach(el => io.observe(el));

// ── Counter animation
const counters = document.querySelectorAll('.stat-counter');
const counterIO = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const el = e.target;
      const target = +el.dataset.target;
      let start = 0;
      const step = () => {
        start = Math.min(start + 1, target);
        el.textContent = start;
        if (start < target) setTimeout(step, 80);
      };
      step();
      counterIO.unobserve(el);
    }
  });
}, { threshold: .5 });
counters.forEach(el => counterIO.observe(el));

// ── Card mouse glow
document.querySelectorAll('[data-card]').forEach(card => {
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    card.style.setProperty('--mx', ((e.clientX - rect.left) / rect.width * 100) + '%');
    card.style.setProperty('--my', ((e.clientY - rect.top) / rect.height * 100) + '%');
  });
});

// ── Nav active
window.addEventListener('scroll', () => {
  const nav = document.querySelector('.nav');
  if (window.scrollY > 40) nav.style.background = 'rgba(3,7,18,.95)';
  else nav.style.background = 'rgba(3,7,18,.8)';
});
</script>
</body>
</html>
