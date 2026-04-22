<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>IFFAT — Frontend Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,500;0,700;1,400&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0d0d0d;
    --bg2: #111111;
    --bg3: #161616;
    --border: #1f1f1f;
    --border-bright: #2a2a2a;
    --accent: #E8593C;
    --accent2: #c94a30;
    --accent-glow: rgba(232,89,60,0.15);
    --accent-dim: rgba(232,89,60,0.06);
    --text: #cccccc;
    --text-muted: #555555;
    --text-dim: #333333;
    --green: #4a9e6b;
    --mono: 'JetBrains Mono', monospace;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--mono);
    font-size: 13px;
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none;
    z-index: 9999;
  }

  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 40px 24px 80px;
  }

  /* ── HEADER ── */
  .header {
    text-align: center;
    padding: 60px 0 50px;
    position: relative;
    border-bottom: 1px solid var(--border);
    margin-bottom: 48px;
  }

  .header-name {
    font-family: 'Space Mono', monospace;
    font-size: clamp(52px, 10vw, 96px);
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 0.18em;
    line-height: 1;
    text-shadow: 0 0 60px rgba(232,89,60,0.4), 0 0 120px rgba(232,89,60,0.15);
    animation: flicker 8s infinite;
  }

  @keyframes flicker {
    0%,95%,100% { opacity: 1; }
    96% { opacity: 0.92; }
    97% { opacity: 1; }
    98% { opacity: 0.88; }
    99% { opacity: 1; }
  }

  .header-sub {
    margin-top: 16px;
    color: var(--text-muted);
    font-size: 11px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
  }

  .header-sub span {
    margin: 0 12px;
  }

  .header-sub span:not(:last-child)::after {
    content: ' ·';
    color: var(--text-dim);
  }

  .typing-line {
    margin-top: 24px;
    color: var(--accent);
    font-size: 13px;
    min-height: 20px;
    opacity: 0.85;
  }

  .typing-line::after {
    content: '▌';
    animation: blink 1s step-end infinite;
  }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ── SECTION LABEL ── */
  .section-label {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 16px;
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }

  .section-label::before {
    content: '◈';
    font-size: 10px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── BENTO GRID ── */
  .bento-row {
    display: grid;
    gap: 12px;
    margin-bottom: 12px;
  }

  .bento-row.col-2 { grid-template-columns: 1fr 1fr; }
  .bento-row.col-3 { grid-template-columns: 1fr 1fr 1fr; }
  .bento-row.col-6-4 { grid-template-columns: 3fr 2fr; }
  .bento-row.col-4-6 { grid-template-columns: 2fr 3fr; }

  .card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 20px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.2s, background 0.2s;
  }

  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .card:hover { border-color: var(--border-bright); background: var(--bg3); }
  .card:hover::before { opacity: 1; }

  /* ── WHOAMI CARD ── */
  .whoami-block {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 16px;
    font-size: 12px;
  }

  .whoami-block .comment { color: var(--text-muted); }
  .whoami-block .key { color: #7a8b99; }
  .whoami-block .val-str { color: #a8c09a; }
  .whoami-block .val-arr { color: var(--accent); }
  .whoami-block .punc { color: var(--text-muted); }

  .quote-line {
    margin-top: 16px;
    padding: 12px;
    border-left: 2px solid var(--accent);
    color: var(--text-muted);
    font-size: 11.5px;
    font-style: italic;
    background: var(--accent-dim);
  }

  /* ── STATUS CARD ── */
  .status-grid {
    display: flex;
    flex-direction: column;
    gap: 8px;
    font-size: 12px;
  }

  .status-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 6px 10px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 2px;
  }

  .status-key { color: var(--text-muted); font-size: 10px; letter-spacing: 0.1em; text-transform: uppercase; }
  .status-val { color: var(--text); font-size: 11px; }
  .status-val.online { color: var(--green); }
  .status-val.accent { color: var(--accent); }

  .online-dot {
    display: inline-block;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--green);
    margin-right: 6px;
    box-shadow: 0 0 6px var(--green);
    animation: pulse 2s infinite;
  }

  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.5} }

  .energy-bar {
    display: flex;
    gap: 3px;
    align-items: center;
  }

  .energy-bar-fill {
    display: flex;
    gap: 2px;
  }

  .e-block {
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 1px;
    opacity: 0.9;
  }

  .e-block.empty {
    background: var(--border-bright);
    opacity: 1;
  }

  /* ── STACK ── */
  .stack-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }

  .stack-col {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 14px 12px;
  }

  .stack-col-title {
    font-size: 10px;
    color: var(--text-muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 12px;
    border-bottom: 1px solid var(--border);
    padding-bottom: 8px;
  }

  .stack-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .tag {
    font-size: 10px;
    padding: 3px 8px;
    border-radius: 2px;
    border: 1px solid;
    letter-spacing: 0.05em;
  }

  .tag.active { border-color: var(--accent); color: var(--accent); background: var(--accent-dim); }
  .tag.mid { border-color: #3a3a3a; color: #666; background: transparent; }
  .tag.dim { border-color: #2a2a2a; color: #444; background: transparent; }
  .tag.white { border-color: #3a3a3a; color: #888; background: transparent; }

  /* ── STATS ── */
  .stat-big {
    text-align: center;
    padding: 24px 16px;
  }

  .stat-num {
    font-family: 'Space Mono', monospace;
    font-size: 42px;
    font-weight: 700;
    color: var(--accent);
    line-height: 1;
    text-shadow: 0 0 30px rgba(232,89,60,0.3);
  }

  .stat-num.loading { font-size: 24px; opacity: 0.4; }

  .stat-label {
    margin-top: 8px;
    font-size: 10px;
    color: var(--text-muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }

  /* ── ACTIVITY GRAPH ── */
  .contrib-grid {
    display: flex;
    gap: 3px;
    flex-wrap: nowrap;
    overflow-x: auto;
    padding-bottom: 4px;
  }

  .contrib-week {
    display: flex;
    flex-direction: column;
    gap: 3px;
  }

  .contrib-day {
    width: 10px; height: 10px;
    border-radius: 1px;
    background: var(--border);
    flex-shrink: 0;
  }

  .contrib-day.l1 { background: rgba(232,89,60,0.25); }
  .contrib-day.l2 { background: rgba(232,89,60,0.5); }
  .contrib-day.l3 { background: rgba(232,89,60,0.75); }
  .contrib-day.l4 { background: var(--accent); }

  /* ── QUEUE ── */
  .queue-items {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .queue-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 10px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 2px;
    font-size: 11px;
  }

  .queue-name { color: var(--text); }
  .queue-badge {
    font-size: 9px;
    padding: 2px 7px;
    border-radius: 2px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .badge-ongoing { background: rgba(232,89,60,0.15); color: var(--accent); border: 1px solid var(--accent); }
  .badge-active  { background: rgba(74,158,107,0.1); color: var(--green); border: 1px solid var(--green); }
  .badge-build   { background: rgba(150,150,80,0.1); color: #b0a040; border: 1px solid #504830; }

  .skill-bars { margin-top: 14px; display: flex; flex-direction: column; gap: 8px; }

  .skill-row { display: flex; flex-direction: column; gap: 4px; }

  .skill-meta {
    display: flex;
    justify-content: space-between;
    font-size: 10px;
    color: var(--text-muted);
  }

  .skill-bar-bg {
    height: 4px;
    background: var(--border);
    border-radius: 2px;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    background: var(--accent);
    border-radius: 2px;
    transition: width 1s ease;
  }

  /* ── PHILOSOPHY ── */
  .philosophy-box {
    text-align: center;
    padding: 32px;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 4px;
    position: relative;
  }

  .philosophy-box::before,
  .philosophy-box::after {
    content: '';
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    width: 60%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
  }

  .philosophy-box::before { top: 0; }
  .philosophy-box::after { bottom: 0; }

  .philosophy-main {
    font-family: 'Space Mono', monospace;
    font-size: 15px;
    color: var(--text);
    line-height: 1.7;
  }

  .philosophy-main em {
    color: var(--accent);
    font-style: normal;
  }

  .philosophy-sub {
    margin-top: 12px;
    font-size: 11px;
    color: var(--text-muted);
    letter-spacing: 0.05em;
  }

  /* ── CONNECT ── */
  .connect-links {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-top: 10px;
  }

  .connect-link {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 14px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--text);
    text-decoration: none;
    font-size: 11px;
    transition: border-color 0.2s, color 0.2s;
  }

  .connect-link:hover { border-color: var(--accent); color: var(--accent); }

  .connect-arrow { color: var(--accent); margin-right: 4px; }

  .open-to {
    margin-top: 14px;
    font-size: 11px;
    color: var(--text-muted);
    line-height: 1.9;
  }

  /* ── FOOTER CARD ── */
  .footer-box {
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 20px;
    text-align: center;
  }

  .footer-name {
    font-family: 'Space Mono', monospace;
    font-size: 18px;
    color: var(--accent);
    letter-spacing: 0.15em;
  }

  .footer-role {
    margin-top: 6px;
    font-size: 10px;
    color: var(--text-muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }

  .footer-tagline {
    margin-top: 16px;
    font-size: 11px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    padding-top: 14px;
    border-top: 1px solid var(--border);
  }

  /* ── PAGE FOOTER ── */
  .page-footer {
    text-align: center;
    margin-top: 60px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    font-size: 10px;
    color: var(--text-dim);
    letter-spacing: 0.2em;
  }

  /* ── REPOS SECTION ── */
  .repo-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }

  .repo-card {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 14px;
    transition: border-color 0.2s;
    cursor: pointer;
    text-decoration: none;
    display: block;
  }

  .repo-card:hover { border-color: var(--border-bright); }
  .repo-card:hover .repo-name { color: var(--accent); }

  .repo-name {
    font-size: 12px;
    color: var(--text);
    margin-bottom: 6px;
    transition: color 0.2s;
  }

  .repo-desc {
    font-size: 10.5px;
    color: var(--text-muted);
    margin-bottom: 10px;
    line-height: 1.5;
  }

  .repo-meta {
    display: flex;
    gap: 12px;
    font-size: 10px;
    color: var(--text-dim);
  }

  .repo-lang { color: var(--accent); }

  /* ── LOADING ── */
  .skeleton {
    background: linear-gradient(90deg, var(--bg2) 25%, var(--bg3) 50%, var(--bg2) 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s infinite;
    border-radius: 2px;
    height: 14px;
  }

  @keyframes shimmer { 0%{background-position:200% 0} 100%{background-position:-200% 0} }

  /* ── TROPHIES ── */
  .trophies {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    justify-content: center;
  }

  .trophy {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
    padding: 14px 18px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    min-width: 80px;
  }

  .trophy-icon { font-size: 20px; }
  .trophy-val  { font-family: 'Space Mono', monospace; font-size: 18px; color: var(--accent); }
  .trophy-lbl  { font-size: 9px; color: var(--text-muted); letter-spacing: 0.15em; text-transform: uppercase; }

  /* Responsive */
  @media (max-width: 600px) {
    .bento-row.col-2,
    .bento-row.col-3,
    .bento-row.col-6-4,
    .bento-row.col-4-6 { grid-template-columns: 1fr; }
    .stack-grid { grid-template-columns: repeat(2, 1fr); }
    .repo-grid { grid-template-columns: 1fr; }
  }

  /* Animations */
  .fade-in {
    opacity: 0;
    transform: translateY(12px);
    animation: fadeUp 0.5s ease forwards;
  }

  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }
</style>
</head>
<body>

<div class="container">

  <!-- HEADER -->
  <header class="header fade-in">
    <div class="header-name">I F F A T</div>
    <div class="header-sub">
      <span>Frontend Developer</span>
      <span>UI/UX Designer</span>
      <span>Builder</span>
    </div>
    <div class="typing-line" id="typing"></div>
  </header>

  <!-- ROW 1: WHOAMI + STATUS -->
  <div class="section-label">whoami</div>
  <div class="bento-row col-6-4" style="margin-bottom:32px; animation: fadeUp 0.5s 0.1s ease both;">
    <div class="card">
      <div class="whoami-block">
        <div><span class="comment">// identity.ts</span></div>
        <div><span class="punc">const </span><span style="color:#7a8b99">iffat</span><span class="punc"> = {</span></div>
        <div>&nbsp;&nbsp;<span class="key">role</span><span class="punc">    : </span><span class="val-str">"Frontend Developer"</span><span class="punc">,</span></div>
        <div>&nbsp;&nbsp;<span class="key">focus</span><span class="punc">   : </span><span class="val-arr">["React", "UI/UX", "Clean Code"]</span><span class="punc">,</span></div>
        <div>&nbsp;&nbsp;<span class="key">learning</span><span class="punc">: </span><span class="val-arr">["API Integration", "DSA / C++"]</span><span class="punc">,</span></div>
        <div>&nbsp;&nbsp;<span class="key">belief</span><span class="punc">  : </span><span class="val-str">"Ship it. Learn. Repeat."</span><span class="punc">,</span></div>
        <div>&nbsp;&nbsp;<span class="key">vibe</span><span class="punc">    : </span><span class="val-str">"design-obsessed · pixel-precise"</span></div>
        <div><span class="punc">}</span></div>
      </div>
      <div class="quote-line">
        "Good design is when the user doesn't have to think.<br/>
        Great design is when they smile."
      </div>
    </div>

    <div class="card">
      <div class="section-label" style="margin-bottom:14px;">status</div>
      <div class="status-grid">
        <div class="status-row">
          <span class="status-key">System</span>
          <span class="status-val online"><span class="online-dot"></span>ONLINE</span>
        </div>
        <div class="status-row">
          <span class="status-key">Mode</span>
          <span class="status-val">building</span>
        </div>
        <div class="status-row">
          <span class="status-key">Focus</span>
          <span class="status-val accent">frontend</span>
        </div>
        <div class="status-row">
          <span class="status-key">Mood</span>
          <span class="status-val">in the zone</span>
        </div>
        <div class="status-row">
          <span class="status-key">Energy</span>
          <span class="status-val">
            <div class="energy-bar">
              <div class="energy-bar-fill" id="energyBar"></div>
            </div>
          </span>
        </div>
      </div>
    </div>
  </div>

  <!-- ROW 2: STACK -->
  <div class="section-label">stack</div>
  <div class="card" style="margin-bottom:32px; animation: fadeUp 0.5s 0.2s ease both;">
    <div class="stack-grid">
      <div class="stack-col">
        <div class="stack-col-title">[ Frontend ]</div>
        <div class="stack-tags">
          <span class="tag active">React</span>
          <span class="tag active">JavaScript</span>
          <span class="tag active">HTML5</span>
          <span class="tag active">CSS3</span>
          <span class="tag active">Figma</span>
        </div>
      </div>
      <div class="stack-col">
        <div class="stack-col-title">[ Backend ]</div>
        <div class="stack-tags">
          <span class="tag mid">Node.js</span>
          <span class="tag mid">Express</span>
          <span class="tag mid">MySQL</span>
          <span class="tag mid">Firebase</span>
        </div>
      </div>
      <div class="stack-col">
        <div class="stack-col-title">[ Languages ]</div>
        <div class="stack-tags">
          <span class="tag dim">C++</span>
          <span class="tag dim">C</span>
          <span class="tag dim">Java</span>
          <span class="tag dim">Python</span>
        </div>
      </div>
      <div class="stack-col">
        <div class="stack-col-title">[ Deploy ]</div>
        <div class="stack-tags">
          <span class="tag white">Vercel</span>
          <span class="tag white">Netlify</span>
          <span class="tag white">Render</span>
          <span class="tag active">Git</span>
        </div>
      </div>
    </div>
  </div>

  <!-- ROW 3: METRICS -->
  <div class="section-label">metrics</div>
  <div class="bento-row col-3" style="margin-bottom:12px; animation: fadeUp 0.5s 0.3s ease both;">
    <div class="card stat-big">
      <div class="stat-num" id="stat-commits">—</div>
      <div class="stat-label">Total Commits</div>
    </div>
    <div class="card stat-big">
      <div class="stat-num" id="stat-repos">—</div>
      <div class="stat-label">Public Repos</div>
    </div>
    <div class="card stat-big">
      <div class="stat-num" id="stat-followers">—</div>
      <div class="stat-label">Followers</div>
    </div>
  </div>

  <div class="bento-row col-3" style="margin-bottom:32px; animation: fadeUp 0.5s 0.35s ease both;">
    <div class="card stat-big">
      <div class="stat-num" id="stat-stars">—</div>
      <div class="stat-label">Total Stars</div>
    </div>
    <div class="card stat-big">
      <div class="stat-num" id="stat-prs">—</div>
      <div class="stat-label">Pull Requests</div>
    </div>
    <div class="card stat-big">
      <div class="stat-num" id="stat-streak">—</div>
      <div class="stat-label">Day Streak</div>
    </div>
  </div>

  <!-- ROW 4: ACTIVITY + QUEUE -->
  <div class="section-label">activity</div>
  <div class="bento-row col-6-4" style="margin-bottom:32px; animation: fadeUp 0.5s 0.4s ease both;">
    <div class="card">
      <div class="section-label" style="font-size:10px; margin-bottom:14px;">contribution graph</div>
      <div class="contrib-grid" id="contribGrid">
        <!-- generated by JS -->
      </div>
      <div style="margin-top:10px; display:flex; gap:6px; align-items:center; font-size:10px; color:var(--text-muted);">
        <span>Less</span>
        <div style="width:10px;height:10px;border-radius:1px;background:var(--border)"></div>
        <div style="width:10px;height:10px;border-radius:1px;background:rgba(232,89,60,0.25)"></div>
        <div style="width:10px;height:10px;border-radius:1px;background:rgba(232,89,60,0.5)"></div>
        <div style="width:10px;height:10px;border-radius:1px;background:rgba(232,89,60,0.75)"></div>
        <div style="width:10px;height:10px;border-radius:1px;background:var(--accent)"></div>
        <span>More</span>
      </div>
    </div>

    <div class="card">
      <div class="section-label" style="font-size:10px; margin-bottom:14px;">queue</div>
      <div class="queue-items">
        <div class="queue-item">
          <span class="queue-name">▸ DSA in C++</span>
          <span class="queue-badge badge-ongoing">Ongoing</span>
        </div>
        <div class="queue-item">
          <span class="queue-name">▸ API Integ.</span>
          <span class="queue-badge badge-active">Active</span>
        </div>
        <div class="queue-item">
          <span class="queue-name">▸ Portfolio</span>
          <span class="queue-badge badge-build">Build</span>
        </div>
      </div>
      <div class="skill-bars">
        <div class="skill-row">
          <div class="skill-meta"><span>React</span><span>82%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" style="width:82%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>UI/UX</span><span>74%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" style="width:74%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>DSA</span><span>50%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" style="width:50%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>Node.js</span><span>45%</span></div>
          <div class="skill-bar-bg"><div class="skill-bar-fill" style="width:45%"></div></div>
        </div>
      </div>
    </div>
  </div>

  <!-- TOP REPOS -->
  <div class="section-label">pinned repos</div>
  <div class="repo-grid" id="repoGrid" style="margin-bottom:32px; animation: fadeUp 0.5s 0.45s ease both;">
    <div class="repo-card"><div class="skeleton"></div><div class="skeleton" style="margin-top:8px;width:70%"></div></div>
    <div class="repo-card"><div class="skeleton"></div><div class="skeleton" style="margin-top:8px;width:70%"></div></div>
    <div class="repo-card"><div class="skeleton"></div><div class="skeleton" style="margin-top:8px;width:70%"></div></div>
    <div class="repo-card"><div class="skeleton"></div><div class="skeleton" style="margin-top:8px;width:70%"></div></div>
  </div>

  <!-- PHILOSOPHY -->
  <div style="margin-bottom:32px; animation: fadeUp 0.5s 0.5s ease both;">
    <div class="philosophy-box">
      <div class="philosophy-main">
        "I don't write code that just works.<br/>
        I write code that <em>looks like it was meant to be there.</em>"
      </div>
      <div class="philosophy-sub">
        Every pixel. Every spacing call. Every hover state. <em style="color:var(--accent);font-style:normal;">Intentional.</em>
      </div>
    </div>
  </div>

  <!-- TROPHIES -->
  <div class="section-label">achievements</div>
  <div class="card" style="margin-bottom:32px; animation: fadeUp 0.5s 0.55s ease both;">
    <div class="trophies" id="trophies">
      <div class="trophy"><div class="trophy-icon">🏆</div><div class="trophy-val" id="t-commits">—</div><div class="trophy-lbl">Commits</div></div>
      <div class="trophy"><div class="trophy-icon">📦</div><div class="trophy-val" id="t-repos">—</div><div class="trophy-lbl">Repos</div></div>
      <div class="trophy"><div class="trophy-icon">⭐</div><div class="trophy-val" id="t-stars">—</div><div class="trophy-lbl">Stars</div></div>
      <div class="trophy"><div class="trophy-icon">👥</div><div class="trophy-val" id="t-followers">—</div><div class="trophy-lbl">Followers</div></div>
      <div class="trophy"><div class="trophy-icon">🔀</div><div class="trophy-val" id="t-prs">—</div><div class="trophy-lbl">Pull Reqs</div></div>
    </div>
  </div>

  <!-- CONNECT + FOOTER -->
  <div class="section-label">connect</div>
  <div class="bento-row col-2" style="animation: fadeUp 0.5s 0.6s ease both;">
    <div class="card">
      <div class="connect-links">
        <a href="https://github.com/IffatK" target="_blank" class="connect-link">
          <span class="connect-arrow">→</span>
          <span>github.com/IffatK</span>
        </a>
        <a href="https://linkedin.com/in/iffat" target="_blank" class="connect-link">
          <span class="connect-arrow">→</span>
          <span>linkedin.com/in/iffat</span>
        </a>
      </div>
      <div class="open-to">
        <span style="color:var(--text-muted)">→</span> Always open to:<br/>
        &nbsp;&nbsp;· Frontend collabs<br/>
        &nbsp;&nbsp;· UI/UX feedback &amp; critique<br/>
        &nbsp;&nbsp;· Cool projects worth building
      </div>
    </div>

    <div class="card footer-box">
      <div class="footer-name">IFFAT.DEV</div>
      <div class="footer-role">Frontend · UI/UX · Code</div>
      <div class="footer-tagline">// "AND THIS IS ME."</div>
    </div>
  </div>

  <div class="page-footer">
    // END OF FILE · THANKS FOR VISITING &nbsp;·&nbsp; <span id="viewCount" style="color:var(--accent)">loading...</span> profile views
  </div>

</div>

<script>
const USERNAME = 'IffatK';
const API = 'https://api.github.com';

// ── Typing animation
const lines = [
  '// design-obsessed. pixel-precise. always building.',
  '// you learn by shipping, not watching.',
  '// making things that look like they belong.'
];
let li = 0, ci = 0, dir = 1, pause = 0;
const el = document.getElementById('typing');

function typeLoop() {
  if (pause > 0) { pause--; setTimeout(typeLoop, 50); return; }
  if (dir === 1) {
    el.textContent = lines[li].slice(0, ++ci);
    if (ci >= lines[li].length) { dir = -1; pause = 40; }
  } else {
    el.textContent = lines[li].slice(0, --ci);
    if (ci <= 0) { li = (li + 1) % lines.length; dir = 1; pause = 10; }
  }
  setTimeout(typeLoop, dir === 1 ? 45 : 20);
}
typeLoop();

// ── Energy bar
function buildEnergy() {
  const bar = document.getElementById('energyBar');
  const filled = 6, total = 8;
  for (let i = 0; i < total; i++) {
    const b = document.createElement('div');
    b.className = 'e-block' + (i >= filled ? ' empty' : '');
    bar.appendChild(b);
  }
}
buildEnergy();

// ── Counter animation
function animateCount(el, target) {
  let start = 0;
  const step = Math.ceil(target / 40);
  const t = setInterval(() => {
    start = Math.min(start + step, target);
    el.textContent = start >= 1000 ? (start/1000).toFixed(1) + 'k' : start;
    if (start >= target) clearInterval(t);
  }, 30);
}

// ── Contribution graph (visual placeholder — GitHub doesn't expose this via REST)
function buildContribGraph() {
  const grid = document.getElementById('contribGrid');
  grid.innerHTML = '';
  const weeks = 26;
  for (let w = 0; w < weeks; w++) {
    const col = document.createElement('div');
    col.className = 'contrib-week';
    for (let d = 0; d < 7; d++) {
      const cell = document.createElement('div');
      const r = Math.random();
      let lvl = 'contrib-day';
      if (r > 0.85) lvl += ' l4';
      else if (r > 0.65) lvl += ' l3';
      else if (r > 0.45) lvl += ' l2';
      else if (r > 0.3) lvl += ' l1';
      cell.className = lvl;
      col.appendChild(cell);
    }
    grid.appendChild(col);
  }
}
buildContribGraph();

// ── Fetch GitHub data
async function fetchGitHub() {
  try {
    const [userRes, reposRes] = await Promise.all([
      fetch(`${API}/users/${USERNAME}`),
      fetch(`${API}/users/${USERNAME}/repos?per_page=100&sort=updated`)
    ]);
    const user = await userRes.json();
    const repos = await reposRes.json();

    // Stats
    const totalStars = repos.reduce((s, r) => s + r.stargazers_count, 0);

    // Update metrics
    animateCount(document.getElementById('stat-repos'), user.public_repos || 0);
    animateCount(document.getElementById('stat-followers'), user.followers || 0);
    animateCount(document.getElementById('stat-stars'), totalStars);

    // Trophy mirrors
    document.getElementById('t-repos').textContent = user.public_repos || 0;
    document.getElementById('t-followers').textContent = user.followers || 0;
    document.getElementById('t-stars').textContent = totalStars;

    // Commits via search API
    const commitRes = await fetch(`${API}/search/commits?q=author:${USERNAME}&per_page=1`, {
      headers: { 'Accept': 'application/vnd.github.cloak-preview' }
    });
    const commitData = await commitRes.json();
    const commits = commitData.total_count || 0;
    animateCount(document.getElementById('stat-commits'), commits);
    document.getElementById('t-commits').textContent = commits >= 1000 ? (commits/1000).toFixed(1) + 'k' : commits;

    // PRs
    const prRes = await fetch(`${API}/search/issues?q=type:pr+author:${USERNAME}&per_page=1`);
    const prData = await prRes.json();
    const prs = prData.total_count || 0;
    animateCount(document.getElementById('stat-prs'), prs);
    document.getElementById('t-prs').textContent = prs;

    // Streak (approximate: count recent commit days)
    const eventsRes = await fetch(`${API}/users/${USERNAME}/events?per_page=100`);
    const events = await eventsRes.json();
    let streak = 0;
    const seen = new Set();
    (Array.isArray(events) ? events : []).forEach(e => {
      if (e.type === 'PushEvent') {
        const day = e.created_at?.slice(0, 10);
        if (day) seen.add(day);
      }
    });
    // Count consecutive days from today backwards
    const today = new Date();
    for (let i = 0; i < 30; i++) {
      const d = new Date(today);
      d.setDate(d.getDate() - i);
      const key = d.toISOString().slice(0, 10);
      if (seen.has(key)) streak++;
      else if (i > 0) break;
    }
    animateCount(document.getElementById('stat-streak'), streak || seen.size);

    // Top repos
    const sorted = repos
      .filter(r => !r.fork)
      .sort((a, b) => b.stargazers_count - a.stargazers_count)
      .slice(0, 6);

    const grid = document.getElementById('repoGrid');
    grid.innerHTML = '';
    (sorted.length ? sorted : repos.slice(0, 6)).forEach(r => {
      const a = document.createElement('a');
      a.href = r.html_url;
      a.target = '_blank';
      a.className = 'repo-card';
      a.innerHTML = `
        <div class="repo-name">📁 ${r.name}</div>
        <div class="repo-desc">${r.description || 'No description provided.'}</div>
        <div class="repo-meta">
          <span class="repo-lang">${r.language || 'N/A'}</span>
          <span>⭐ ${r.stargazers_count}</span>
          <span>🍴 ${r.forks_count}</span>
        </div>
      `;
      grid.appendChild(a);
    });

  } catch(e) {
    console.error('GitHub fetch error:', e);
    ['stat-commits','stat-repos','stat-followers','stat-stars','stat-prs','stat-streak'].forEach(id => {
      const el = document.getElementById(id);
      if (el) el.textContent = '—';
    });
  }
}

fetchGitHub();

// ── Profile view count (localStorage counter)
const views = parseInt(localStorage.getItem('iffat_views') || '0') + 1;
localStorage.setItem('iffat_views', views);
document.getElementById('viewCount').textContent = views.toLocaleString();
</script>
</body>
</html>
