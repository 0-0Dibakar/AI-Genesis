<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AIGenesis — AI-Powered Internship Platform</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #080C14;
    --bg2: #0D1220;
    --bg3: #111827;
    --accent: #00F5C4;
    --accent2: #7C6FFF;
    --accent3: #FF6B6B;
    --text: #F0F4FF;
    --muted: #8A96B0;
    --border: rgba(255,255,255,0.08);
    --glass: rgba(255,255,255,0.04);
    --glass2: rgba(255,255,255,0.07);
    --card-border: rgba(0,245,196,0.15);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 16px;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem 3rem;
    background: rgba(8,12,20,0.85);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-size: 1.4rem;
    font-weight: 800;
    letter-spacing: -0.02em;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 400;
    transition: color 0.2s;
    letter-spacing: 0.01em;
  }

  .nav-links a:hover { color: var(--text); }

  .nav-cta {
    background: linear-gradient(135deg, var(--accent), #00D4A8);
    color: #080C14 !important;
    padding: 0.5rem 1.25rem;
    border-radius: 6px;
    font-weight: 600 !important;
    font-size: 0.85rem !important;
    -webkit-text-fill-color: #080C14 !important;
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 8rem 2rem 4rem;
    position: relative;
    overflow: hidden;
  }

  /* ORB BACKGROUNDS */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
  }

  .orb-1 {
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,245,196,0.12) 0%, transparent 70%);
    top: -100px; left: -100px;
    animation: orbFloat 8s ease-in-out infinite;
  }

  .orb-2 {
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(124,111,255,0.15) 0%, transparent 70%);
    bottom: 0; right: -50px;
    animation: orbFloat 10s ease-in-out infinite reverse;
  }

  .orb-3 {
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(255,107,107,0.08) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
  }

  @keyframes orbFloat {
    0%, 100% { transform: translateY(0px) scale(1); }
    50% { transform: translateY(-30px) scale(1.05); }
  }

  /* BADGE */
  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    background: rgba(0,245,196,0.08);
    border: 1px solid rgba(0,245,196,0.2);
    color: var(--accent);
    padding: 0.35rem 1rem;
    border-radius: 100px;
    font-size: 0.8rem;
    font-weight: 500;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.6s ease both;
  }

  .badge-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    animation: pulse 2s ease infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.8); }
  }

  /* HERO HEADLINE */
  .hero-headline {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.8rem, 6vw, 5.5rem);
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -0.03em;
    max-width: 900px;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.6s 0.1s ease both;
  }

  .hero-headline .highlight {
    background: linear-gradient(90deg, var(--accent) 0%, var(--accent2) 50%, var(--accent3) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-sub {
    font-size: clamp(1rem, 2vw, 1.2rem);
    color: var(--muted);
    max-width: 580px;
    margin: 1.5rem auto 0;
    font-weight: 300;
    line-height: 1.7;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.6s 0.2s ease both;
  }

  .hero-ctas {
    display: flex;
    gap: 1rem;
    justify-content: center;
    margin-top: 2.5rem;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.6s 0.3s ease both;
    flex-wrap: wrap;
  }

  .btn-primary {
    background: linear-gradient(135deg, var(--accent), #00D4A8);
    color: #080C14;
    padding: 0.85rem 2rem;
    border-radius: 8px;
    font-weight: 600;
    font-size: 0.95rem;
    text-decoration: none;
    border: none;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
    letter-spacing: 0.01em;
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 40px rgba(0,245,196,0.3);
  }

  .btn-ghost {
    background: transparent;
    color: var(--text);
    padding: 0.85rem 2rem;
    border-radius: 8px;
    font-weight: 500;
    font-size: 0.95rem;
    text-decoration: none;
    border: 1px solid var(--border);
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s;
  }

  .btn-ghost:hover {
    border-color: rgba(255,255,255,0.2);
    background: var(--glass);
  }

  /* STATS BAR */
  .stats-bar {
    display: flex;
    gap: 0;
    justify-content: center;
    margin-top: 4rem;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.6s 0.4s ease both;
    background: var(--glass);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    max-width: 700px;
    width: 100%;
  }

  .stat-item {
    flex: 1;
    padding: 1.25rem 1rem;
    text-align: center;
    border-right: 1px solid var(--border);
  }

  .stat-item:last-child { border-right: none; }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 1.6rem;
    font-weight: 700;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .stat-label {
    font-size: 0.78rem;
    color: var(--muted);
    margin-top: 0.2rem;
    letter-spacing: 0.03em;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* SECTION COMMON */
  section {
    padding: 6rem 2rem;
    position: relative;
    z-index: 1;
  }

  .container {
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-label {
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 0.75rem;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 700;
    letter-spacing: -0.03em;
    line-height: 1.1;
    margin-bottom: 1rem;
  }

  .section-desc {
    color: var(--muted);
    font-size: 1rem;
    max-width: 560px;
    line-height: 1.7;
    font-weight: 300;
  }

  /* HOW IT WORKS */
  .phases {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .phase-card {
    background: var(--glass);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
  }

  .phase-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,245,196,0.03), transparent);
    pointer-events: none;
  }

  .phase-card:hover {
    border-color: var(--card-border);
    transform: translateY(-4px);
  }

  .phase-card.phase2::before {
    background: linear-gradient(135deg, rgba(124,111,255,0.05), transparent);
  }

  .phase-card.phase2 { border-color: rgba(124,111,255,0.15); }

  .phase-num {
    font-family: 'Syne', sans-serif;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 0.5rem;
  }

  .phase-card.phase2 .phase-num { color: var(--accent2); }

  .phase-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.4rem;
    font-weight: 700;
    margin-bottom: 0.75rem;
  }

  .phase-desc {
    color: var(--muted);
    font-size: 0.9rem;
    line-height: 1.7;
    margin-bottom: 1.25rem;
    font-weight: 300;
  }

  .phase-items {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .phase-items li {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    font-size: 0.875rem;
    color: var(--muted);
  }

  .phase-items li::before {
    content: '';
    width: 5px; height: 5px;
    border-radius: 50%;
    background: var(--accent);
    flex-shrink: 0;
  }

  .phase-card.phase2 .phase-items li::before { background: var(--accent2); }

  /* TOOLS GRID */
  .tools-section { background: var(--bg2); }

  .tools-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
    gap: 1rem;
    margin-top: 3rem;
  }

  .tool-chip {
    background: var(--glass);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 0.75rem 0.5rem;
    text-align: center;
    font-size: 0.8rem;
    color: var(--muted);
    font-weight: 400;
    transition: all 0.2s;
    cursor: default;
  }

  .tool-chip:hover {
    border-color: var(--card-border);
    color: var(--text);
    background: var(--glass2);
  }

  .tool-icon {
    font-size: 1.3rem;
    margin-bottom: 0.4rem;
    display: block;
  }

  /* DOMAINS */
  .domains-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 1rem;
    margin-top: 3rem;
  }

  .domain-card {
    background: var(--glass);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.25rem;
    transition: all 0.25s;
    cursor: default;
  }

  .domain-card:hover {
    border-color: var(--card-border);
    background: var(--glass2);
    transform: translateY(-2px);
  }

  .domain-icon {
    width: 36px; height: 36px;
    border-radius: 8px;
    background: rgba(0,245,196,0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.1rem;
    margin-bottom: 0.75rem;
  }

  .domain-name {
    font-size: 0.875rem;
    font-weight: 500;
    color: var(--text);
    line-height: 1.3;
  }

  /* PRICING */
  .pricing-section { background: var(--bg2); }

  .pricing-card {
    max-width: 520px;
    margin: 3rem auto 0;
    background: linear-gradient(135deg, rgba(0,245,196,0.05), rgba(124,111,255,0.05));
    border: 1px solid rgba(0,245,196,0.2);
    border-radius: 20px;
    padding: 2.5rem;
    position: relative;
    overflow: hidden;
    text-align: center;
  }

  .pricing-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }

  .pricing-tag {
    display: inline-block;
    background: rgba(0,245,196,0.1);
    color: var(--accent);
    border: 1px solid rgba(0,245,196,0.2);
    padding: 0.3rem 0.85rem;
    border-radius: 100px;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .pricing-price {
    font-family: 'Syne', sans-serif;
    font-size: 4rem;
    font-weight: 800;
    letter-spacing: -0.04em;
  }

  .pricing-price span {
    font-size: 1.5rem;
    vertical-align: super;
    font-weight: 600;
  }

  .pricing-sub {
    color: var(--muted);
    font-size: 0.875rem;
    margin-top: 0.25rem;
    font-weight: 300;
  }

  .pricing-features {
    list-style: none;
    margin: 1.75rem 0;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    text-align: left;
  }

  .pricing-features li {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-size: 0.9rem;
    color: var(--muted);
  }

  .check-icon {
    width: 18px; height: 18px;
    border-radius: 50%;
    background: rgba(0,245,196,0.15);
    color: var(--accent);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    flex-shrink: 0;
    font-weight: 700;
  }

  /* PROCESS */
  .process-steps {
    display: flex;
    flex-direction: column;
    gap: 0;
    margin-top: 3rem;
    max-width: 600px;
  }

  .process-step {
    display: flex;
    gap: 1.5rem;
    align-items: flex-start;
  }

  .step-connector {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex-shrink: 0;
  }

  .step-num {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: rgba(0,245,196,0.1);
    border: 1px solid rgba(0,245,196,0.25);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.85rem;
    color: var(--accent);
    flex-shrink: 0;
  }

  .step-line {
    width: 1px;
    flex: 1;
    min-height: 40px;
    background: linear-gradient(to bottom, rgba(0,245,196,0.2), transparent);
    margin: 4px 0;
  }

  .process-step:last-child .step-line { display: none; }

  .step-body {
    padding-bottom: 2rem;
  }

  .step-title {
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: 0.3rem;
  }

  .step-desc {
    color: var(--muted);
    font-size: 0.875rem;
    font-weight: 300;
    line-height: 1.6;
  }

  /* CTA SECTION */
  .cta-section {
    background: linear-gradient(135deg, rgba(0,245,196,0.05), rgba(124,111,255,0.05));
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    text-align: center;
    padding: 7rem 2rem;
  }

  .cta-glow {
    position: absolute;
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(0,245,196,0.08), transparent 70%);
    left: 50%; top: 50%;
    transform: translate(-50%, -50%);
    pointer-events: none;
    border-radius: 50%;
  }

  /* FOOTER */
  footer {
    padding: 3rem 2rem;
    border-top: 1px solid var(--border);
  }

  .footer-inner {
    max-width: 1100px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .footer-copy {
    color: var(--muted);
    font-size: 0.85rem;
  }

  .footer-links {
    display: flex;
    gap: 1.5rem;
    list-style: none;
  }

  .footer-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 0.85rem;
    transition: color 0.2s;
  }

  .footer-links a:hover { color: var(--text); }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 3px; }

  /* RESPONSIVE */
  @media (max-width: 700px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .phases { grid-template-columns: 1fr; }
    section { padding: 4rem 1.25rem; }
    .hero { padding: 7rem 1.25rem 3rem; }
  }

  /* INCOME BADGE */
  .income-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    background: rgba(255,107,107,0.1);
    border: 1px solid rgba(255,107,107,0.2);
    color: #FF8C8C;
    padding: 0.3rem 0.85rem;
    border-radius: 100px;
    font-size: 0.78rem;
    font-weight: 600;
    margin-top: 1rem;
  }

  .marquee-track {
    overflow: hidden;
    white-space: nowrap;
    margin-top: 4rem;
    position: relative;
    z-index: 1;
  }

  .marquee-inner {
    display: inline-block;
    animation: marquee 20s linear infinite;
    font-family: 'Syne', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .marquee-inner span {
    margin: 0 2.5rem;
    color: rgba(0,245,196,0.4);
  }

  @keyframes marquee {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">AIGenesis</div>
  <ul class="nav-links">
    <li><a href="#how">How it Works</a></li>
    <li><a href="#domains">Domains</a></li>
    <li><a href="#tools">AI Tools</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#apply" class="nav-cta">Apply Now →</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <div class="hero-badge">
    <div class="badge-dot"></div>
    Now Accepting Applications · Cohort 4
  </div>

  <h1 class="hero-headline">
    Learn AI.<br>
    Build Real Projects.<br>
    <span class="highlight">Get Paid.</span>
  </h1>

  <p class="hero-sub">
    A 60-day remote internship that transforms students and self-taught developers into paid AI builders — with real client projects, expert mentorship, and up to $3,000 in earnings.
  </p>

  <div class="hero-ctas">
    <a href="#apply" class="btn-primary">Apply for Free → $49 Onboarding</a>
    <a href="#how" class="btn-ghost">See How It Works</a>
  </div>

  <div class="income-badge">
    💰 Average stipend: up to $3,000 per cohort
  </div>

  <div class="stats-bar">
    <div class="stat-item">
      <div class="stat-num">60</div>
      <div class="stat-label">Day Program</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">12+</div>
      <div class="stat-label">Tech Domains</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">14+</div>
      <div class="stat-label">Premium AI Tools</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">$3K</div>
      <div class="stat-label">Max Stipend</div>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-track" aria-hidden="true">
  <div class="marquee-inner">
    AI & Machine Learning <span>◆</span> Full Stack Development <span>◆</span> Mobile App Development <span>◆</span> Data Science <span>◆</span> Cybersecurity <span>◆</span> Cloud & DevOps <span>◆</span> UI/UX Design <span>◆</span> Blockchain <span>◆</span> AI Agents & Automation <span>◆</span> Digital Marketing Tech <span>◆</span> Product Management <span>◆</span>
    AI & Machine Learning <span>◆</span> Full Stack Development <span>◆</span> Mobile App Development <span>◆</span> Data Science <span>◆</span> Cybersecurity <span>◆</span> Cloud & DevOps <span>◆</span> UI/UX Design <span>◆</span> Blockchain <span>◆</span> AI Agents & Automation <span>◆</span> Digital Marketing Tech <span>◆</span> Product Management <span>◆</span>
  </div>
</div>

<!-- HOW IT WORKS -->
<section id="how">
  <div class="container">
    <div class="section-label">The Program</div>
    <h2 class="section-title">From Learner to Paid Builder<br>in 60 Days</h2>
    <p class="section-desc">Two structured phases designed to rapidly level up your skills and connect you to real client revenue.</p>

    <div class="phases">
      <!-- PHASE 1 -->
      <div class="phase-card">
        <div class="phase-num">Phase 01 · Month 1</div>
        <div class="phase-title">AI Access & Training</div>
        <p class="phase-desc">Master cutting-edge AI tools through real-world tutorials, mentorship sessions, and collaborative team workflows.</p>
        <ul class="phase-items">
          <li>Access to 14+ premium AI tools</li>
          <li>Guided learning paths per domain</li>
          <li>Weekly live mentorship sessions</li>
          <li>AI workflow & productivity training</li>
          <li>Portfolio building support</li>
          <li>Team collaboration environment</li>
        </ul>
      </div>

      <!-- PHASE 2 -->
      <div class="phase-card phase2">
        <div class="phase-num">Phase 02 · Month 2</div>
        <div class="phase-title">Real Client Projects</div>
        <p class="phase-desc">Get assigned actual client work — build apps, automations, SaaS products, and AI agents in supervised teams.</p>
        <ul class="phase-items">
          <li>Real client project assignments</li>
          <li>AI-assisted development sprints</li>
          <li>Project manager supervision</li>
          <li>Websites, apps, dashboards & agents</li>
          <li>Performance-based stipend</li>
          <li>Portfolio-grade deliverables</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- DOMAINS -->
<section id="domains" style="background: var(--bg2);">
  <div class="container">
    <div class="section-label">Specializations</div>
    <h2 class="section-title">Choose Your Domain</h2>
    <p class="section-desc">12 technology tracks. All remote. All AI-powered. All designed for the future of work.</p>

    <div class="domains-grid">
      <div class="domain-card"><div class="domain-icon">🤖</div><div class="domain-name">AI & Machine Learning</div></div>
      <div class="domain-card"><div class="domain-icon">⚡</div><div class="domain-name">Full Stack Development</div></div>
      <div class="domain-card"><div class="domain-icon">🌐</div><div class="domain-name">Web Development</div></div>
      <div class="domain-card"><div class="domain-icon">📱</div><div class="domain-name">Mobile App Dev</div></div>
      <div class="domain-card"><div class="domain-icon">📊</div><div class="domain-name">Data Science</div></div>
      <div class="domain-card"><div class="domain-icon">🔒</div><div class="domain-name">Cybersecurity</div></div>
      <div class="domain-card"><div class="domain-icon">☁️</div><div class="domain-name">Cloud & DevOps</div></div>
      <div class="domain-card"><div class="domain-icon">🎨</div><div class="domain-name">UI/UX Design</div></div>
      <div class="domain-card"><div class="domain-icon">⛓️</div><div class="domain-name">Blockchain</div></div>
      <div class="domain-card"><div class="domain-icon">🔄</div><div class="domain-name">AI Agents & Automation</div></div>
      <div class="domain-card"><div class="domain-icon">📣</div><div class="domain-name">Digital Marketing Tech</div></div>
      <div class="domain-card"><div class="domain-icon">🗺️</div><div class="domain-name">Product Management</div></div>
    </div>
  </div>
</section>

<!-- AI TOOLS -->
<section id="tools">
  <div class="container">
    <div class="section-label">Your Toolkit</div>
    <h2 class="section-title">14+ Premium AI Tools,<br>Included from Day 1</h2>
    <p class="section-desc">Work with the exact tools used by professional AI teams at top companies worldwide.</p>

    <div class="tools-grid">
      <div class="tool-chip"><span class="tool-icon">🤖</span>ChatGPT</div>
      <div class="tool-chip"><span class="tool-icon">🌟</span>Claude</div>
      <div class="tool-chip"><span class="tool-icon">💎</span>Gemini</div>
      <div class="tool-chip"><span class="tool-icon">⚡</span>Cursor</div>
      <div class="tool-chip"><span class="tool-icon">🎨</span>Midjourney</div>
      <div class="tool-chip"><span class="tool-icon">💻</span>GitHub Copilot</div>
      <div class="tool-chip"><span class="tool-icon">🔍</span>Perplexity</div>
      <div class="tool-chip"><span class="tool-icon">🎙️</span>ElevenLabs</div>
      <div class="tool-chip"><span class="tool-icon">🎬</span>RunwayML</div>
      <div class="tool-chip"><span class="tool-icon">❤️</span>Lovable</div>
      <div class="tool-chip"><span class="tool-icon">🔧</span>Replit</div>
      <div class="tool-chip"><span class="tool-icon">⚡</span>Bolt.new</div>
      <div class="tool-chip"><span class="tool-icon">🚀</span>Vercel AI SDK</div>
      <div class="tool-chip"><span class="tool-icon">🛠️</span>Open Source</div>
    </div>
  </div>
</section>

<!-- APPLICATION PROCESS -->
<section style="background: var(--bg2);">
  <div class="container" style="display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: start;">
    <div>
      <div class="section-label">How to Apply</div>
      <h2 class="section-title">5-Step Selection<br>Process</h2>
      <p class="section-desc">Competitive but fair. We select candidates based on potential, not just experience.</p>
    </div>

    <div class="process-steps">
      <div class="process-step">
        <div class="step-connector"><div class="step-num">1</div><div class="step-line"></div></div>
        <div class="step-body"><div class="step-title">Resume Screening</div><div class="step-desc">Submit your background — we screen for potential and learning attitude, not just credentials.</div></div>
      </div>
      <div class="process-step">
        <div class="step-connector"><div class="step-num">2</div><div class="step-line"></div></div>
        <div class="step-body"><div class="step-title">AI Aptitude Test</div><div class="step-desc">A practical test to assess your problem-solving ability and AI tool familiarity.</div></div>
      </div>
      <div class="process-step">
        <div class="step-connector"><div class="step-num">3</div><div class="step-line"></div></div>
        <div class="step-body"><div class="step-title">Technical Interview</div><div class="step-desc">A focused 30-minute conversation with a domain-specific mentor from our team.</div></div>
      </div>
      <div class="process-step">
        <div class="step-connector"><div class="step-num">4</div><div class="step-line"></div></div>
        <div class="step-body"><div class="step-title">Communication Round</div><div class="step-desc">We assess your written and async communication — crucial for remote AI project work.</div></div>
      </div>
      <div class="process-step">
        <div class="step-connector"><div class="step-num">5</div><div class="step-line"></div></div>
        <div class="step-body"><div class="step-title">Final Selection & Onboarding</div><div class="step-desc">Accepted candidates pay a one-time $49 platform access fee and get immediate tool access.</div></div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing" class="pricing-section">
  <div class="container" style="text-align: center;">
    <div class="section-label">Investment</div>
    <h2 class="section-title">One Fee. Lifetime Impact.</h2>
    <p class="section-desc" style="margin: 0 auto;">One-time onboarding fee unlocks everything — tools, mentors, projects, and your path to earning.</p>

    <div class="pricing-card">
      <div class="pricing-tag">One-Time Onboarding Fee</div>
      <div class="pricing-price"><span>$</span>49</div>
      <div class="pricing-sub">Full 60-day program access · No recurring charges</div>

      <ul class="pricing-features">
        <li><div class="check-icon">✓</div>Access to 14+ premium AI tools</div></li>
        <li><div class="check-icon">✓</div>Structured domain learning paths</div></li>
        <li><div class="check-icon">✓</div>Weekly live mentorship sessions</div></li>
        <li><div class="check-icon">✓</div>Real client project assignment</div></li>
        <li><div class="check-icon">✓</div>Performance-based stipend (up to $3,000)</div></li>
        <li><div class="check-icon">✓</div>Portfolio & certificate on completion</div></li>
        <li><div class="check-icon">✓</div>Community access & peer collaboration</div></li>
        <li><div class="check-icon">✓</div>Referral program & leaderboard rewards</div></li>
      </ul>

      <a href="#apply" class="btn-primary" style="display: block; text-align: center; margin-top: 0.5rem;">Apply Now — Start Your 60-Day Journey</a>
    </div>
  </div>
</section>

<!-- FINAL CTA -->
<section id="apply" class="cta-section" style="position: relative;">
  <div class="cta-glow"></div>
  <div class="container" style="position: relative; z-index: 1;">
    <div class="hero-badge" style="margin: 0 auto 1.5rem;">
      <div class="badge-dot"></div>
      Applications Open · Limited Spots
    </div>
    <h2 class="section-title" style="font-size: clamp(2.2rem, 5vw, 3.8rem); margin-bottom: 1rem;">
      From Learner to Paid<br>AI Builder in 60 Days.
    </h2>
    <p class="section-desc" style="margin: 0 auto 2.5rem; max-width: 500px;">
      Join a global cohort of ambitious developers, students, and freelancers building real things with AI — and getting paid for it.
    </p>
    <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
      <a href="#" class="btn-primary" style="font-size: 1rem; padding: 1rem 2.5rem;">Apply Now →</a>
      <a href="#" class="btn-ghost" style="font-size: 1rem; padding: 1rem 2.5rem;">Learn More</a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="nav-logo">AIGenesis</div>
    <ul class="footer-links">
      <li><a href="#">About</a></li>
      <li><a href="#">Programs</a></li>
      <li><a href="#">Privacy</a></li>
      <li><a href="#">Terms</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
    <div class="footer-copy">© 2026 AIGenesis. All rights reserved.</div>
  </div>
</footer>

</body>
</html>
