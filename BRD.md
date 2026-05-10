<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>APEX | Born from Speed</title>
  
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@300;400;500;600;700&family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap" rel="stylesheet">
  
  <style>
    :root {
      --primary: #E8290B;
      --gold: #D4A017;
      --bg: #090909;
      --surface: #181818;
      --mid: #111111;
      --text: #F0EDE6;
      --muted: #888888;
      --border: rgba(255, 255, 255, 0.08);
      
      --font-display: 'Bebas Neue', sans-serif;
      --font-body: 'Rajdhani', sans-serif;
      --font-mono: 'Space Mono', monospace;
    }
    
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      cursor: none; 
    }
    
    body {
      background-color: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      overflow-x: hidden;
    }
    
    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0; width: 100vw; height: 100vh;
      z-index: 99998;
      pointer-events: none;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
      opacity: 0.04;
    }
    
    #cursor {
      width: 12px; height: 12px;
      background-color: var(--primary);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 99999;
      transform: translate(-50%, -50%);
      mix-blend-mode: difference;
      transition: width 0.2s, height 0.2s;
    }
    
    #cursor-ring {
      width: 36px; height: 36px;
      border: 1px solid var(--primary);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 99999;
      transform: translate(-50%, -50%);
      transition: width 0.2s, height 0.2s, top 0.08s ease-out, left 0.08s ease-out;
    }

    h1, h2, h3, h4, .bebas {
      font-family: var(--font-display);
      font-weight: normal;
      text-transform: uppercase;
      line-height: 1;
    }
    
    .mono { font-family: var(--font-mono); }
    .text-red { color: var(--primary); }
    .text-gold { color: var(--gold); }
    .text-muted { color: var(--muted); }
    
    .btn-red {
      display: inline-block;
      background: var(--primary);
      color: #fff;
      padding: 1rem 2rem;
      text-transform: uppercase;
      font-weight: 600;
      letter-spacing: 1px;
      clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
      text-decoration: none;
      transition: background 0.3s;
    }
    .btn-red:hover { background: #ff3a1a; }
    
    #loader {
      position: fixed;
      top: 0; left: 0; width: 100vw; height: 100vh;
      background: var(--bg);
      z-index: 100000;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      transition: opacity 0.5s ease, transform 0.5s ease;
    }
    
    #loader .logo-loader {
      font-family: var(--font-display);
      font-size: 4rem;
      letter-spacing: 0.2em;
      animation: pulse 1s infinite alternate;
    }
    
    #loader .progress-wrapper {
      width: 200px;
      height: 2px;
      background: var(--surface);
      margin-top: 2rem;
      position: relative;
    }
    
    #loader .progress-bar {
      height: 100%;
      background: var(--primary);
      width: 0%;
      transition: width 0.1s linear;
    }
    
    @keyframes pulse {
      from { opacity: 0.5; }
      to { opacity: 1; }
    }
    
    nav {
      position: fixed;
      top: 0; left: 0; width: 100%;
      padding: 1.5rem 4rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 1000;
      transition: background 0.3s, backdrop-filter 0.3s;
    }
    nav.scrolled {
      background: rgba(9, 9, 9, 0.97);
      backdrop-filter: blur(12px);
    }
    .nav-logo {
      font-family: var(--font-display);
      font-size: 2.5rem;
      text-decoration: none;
      color: var(--text);
    }
    .nav-links {
      display: flex;
      gap: 2rem;
    }
    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      text-transform: uppercase;
      letter-spacing: 0.2em;
      font-size: 0.9rem;
      transition: color 0.3s;
    }
    .nav-links a:hover { color: var(--primary); }
    
    #hero {
      width: 100vw; height: 100vh;
      position: relative;
      overflow: hidden;
      padding: 0;
    }
    #hero-canvas {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
      z-index: 1;
    }
    .hero-content {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
      z-index: 10;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 0 10vw;
      pointer-events: none;
    }
    .hero-content > * { pointer-events: auto; }
    
    .hero-badge {
      color: var(--gold);
      font-family: var(--font-mono);
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 1rem;
      margin-bottom: 2rem;
    }
    .hero-badge::before {
      content: "";
      width: 24px; height: 1px;
      background: var(--gold);
    }
    .hero-h1 {
      font-size: clamp(4.5rem, 10vw, 9rem);
      line-height: 0.9;
      margin-bottom: 1.5rem;
    }
    .hero-sub {
      color: var(--muted);
      max-width: 400px;
      font-size: 1.1rem;
      line-height: 1.6;
      margin-bottom: 3rem;
    }
    .hero-ctas {
      display: flex;
      align-items: center;
      gap: 2rem;
    }
    .ghost-link {
      color: var(--text);
      text-decoration: none;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 1px;
      position: relative;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    .ghost-link::after {
      content: "→";
      transition: transform 0.3s;
    }
    .ghost-link:hover::after {
      transform: translateX(5px);
    }
    .hero-stats {
      position: absolute;
      bottom: 3rem; right: 4rem;
      display: flex;
      gap: 3rem;
      pointer-events: auto;
      z-index: 10;
    }
    .stat-item h3 { font-size: 3rem; }
    .stat-item p {
      font-family: var(--font-mono);
      color: var(--muted);
      font-size: 0.8rem;
      text-transform: uppercase;
    }
    .scroll-indicator {
      position: absolute;
      bottom: 3rem; left: 4rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      pointer-events: auto;
      z-index: 10;
    }
    .scroll-line {
      width: 1px; height: 60px;
      background: linear-gradient(to bottom, var(--primary), transparent);
      animation: scrollPulse 2s infinite;
    }
    .scroll-text {
      writing-mode: vertical-rl;
      font-family: var(--font-mono);
      font-size: 0.7rem;
      color: var(--muted);
      letter-spacing: 0.2em;
    }
    @keyframes scrollPulse {
      0% { transform: scaleY(0); transform-origin: top; opacity: 0; }
      50% { transform: scaleY(1); transform-origin: top; opacity: 1; }
      50.1% { transform: scaleY(1); transform-origin: bottom; opacity: 1; }
      100% { transform: scaleY(0); transform-origin: bottom; opacity: 0; }
    }
    
    #marquee {
      width: 100%;
      background: var(--primary);
      padding: 1rem 0;
      overflow: hidden;
      white-space: nowrap;
      display: flex;
    }
    .marquee-track {
      display: flex;
      animation: marqueeScroll 20s linear infinite;
    }
    .marquee-item {
      font-family: var(--font-mono);
      font-size: 0.7rem;
      color: #fff;
      text-transform: uppercase;
      padding: 0 2rem;
      display: flex;
      align-items: center;
      gap: 2rem;
    }
    .marquee-item::after {
      content: "★";
      color: rgba(255,255,255,0.5);
    }
    @keyframes marqueeScroll {
      0% { transform: translateX(0); }
      100% { transform: translateX(-50%); }
    }
    
    section { padding: 8rem 10vw; }
    .section-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 4rem;
    }
    .section-tag {
      color: var(--primary);
      font-family: var(--font-mono);
      font-size: 0.8rem;
      text-transform: uppercase;
      margin-bottom: 1rem;
      display: block;
    }
    .section-title { font-size: 4rem; }
    
    .models-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5px;
      background: var(--border);
      border: 1px solid var(--border);
    }
    .model-card {
      background: var(--bg);
      aspect-ratio: 4/3;
      position: relative;
      overflow: hidden;
      transition: transform 0.3s;
    }
    .model-card:hover {
      transform: scale(1.01);
      z-index: 2;
    }
    .model-canvas-wrapper {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%;
    }
    .model-badge {
      position: absolute;
      top: 1.5rem; right: 1.5rem;
      color: var(--gold);
      font-family: var(--font-mono);
      font-size: 0.8rem;
      border: 1px solid var(--gold);
      padding: 0.3rem 0.8rem;
      pointer-events: none;
    }
    .model-info {
      position: absolute;
      bottom: 0; left: 0; width: 100%;
      padding: 2rem 1.5rem;
      background: linear-gradient(to top, rgba(9,9,9,0.9), transparent);
      pointer-events: none;
    }
    .model-type {
      background: var(--primary);
      color: #fff;
      font-family: var(--font-mono);
      font-size: 0.7rem;
      padding: 0.2rem 0.5rem;
      display: inline-block;
      margin-bottom: 0.5rem;
    }
    .model-name { font-size: 2rem; margin-bottom: 0.2rem; }
    .model-specs {
      color: var(--muted);
      font-size: 0.85rem;
      font-family: var(--font-mono);
    }

    .specs-layout {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: center;
    }
    .specs-desc {
      color: var(--muted);
      margin-bottom: 3rem;
      font-size: 1.1rem;
      line-height: 1.6;
    }
    .spec-item {
      margin-bottom: 1.5rem;
      position: relative;
    }
    .spec-label {
      color: var(--muted);
      font-family: var(--font-mono);
      font-size: 0.8rem;
      text-transform: uppercase;
      margin-bottom: 0.5rem;
      display: block;
    }
    .spec-bar-bg {
      width: 100%; height: 2px;
      background: var(--surface);
      margin-bottom: 0.5rem;
    }
    .spec-bar-fill {
      height: 100%;
      background: var(--primary);
      width: 0;
      transition: width 1.2s cubic-bezier(0.2, 0.8, 0.2, 1);
    }
    .spec-val { font-size: 1.8rem; }
    .spec-unit {
      color: var(--muted);
      font-family: var(--font-mono);
      font-size: 1rem;
    }
    .spec-item::after {
      content: "";
      position: absolute;
      bottom: -0.5rem; left: 0;
      width: 0; height: 1px;
      background: var(--primary);
      transition: width 0.8s ease;
    }
    .spec-item.active::after { width: 100%; }
    
    .engine-canvas-wrapper {
      width: 100%;
      aspect-ratio: 1;
      background: var(--surface);
      position: relative;
    }

    #experience {
      background: radial-gradient(ellipse at center, rgba(232, 41, 11, 0.05) 0%, transparent 70%);
      text-align: center;
    }
    .features-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1.5px;
      background: var(--border);
      border: 1px solid var(--border);
      margin-top: 4rem;
      text-align: left;
    }
    .feature-cell {
      background: var(--surface);
      padding: 2.5rem;
      transition: background 0.3s, border-color 0.3s;
      border: 1px solid transparent;
    }
    .feature-cell:hover {
      border-color: var(--primary);
      background: rgba(232, 41, 11, 0.02);
    }
    .feature-icon {
      font-size: 2rem;
      margin-bottom: 1.5rem;
      display: block;
    }
    .feature-title {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }
    .feature-desc {
      color: var(--muted);
      font-size: 0.95rem;
      line-height: 1.5;
    }

    .config-layout {
      display: grid;
      grid-template-columns: 1fr 380px;
      gap: 4rem;
    }
    .config-canvas-wrapper {
      aspect-ratio: 16/9;
      background: var(--surface);
      position: relative;
      cursor: grab;
    }
    .config-canvas-wrapper:active { cursor: grabbing; }
    .config-options {
      display: flex;
      flex-direction: column;
      gap: 2rem;
    }
    .config-group-title {
      font-family: var(--font-mono);
      font-size: 0.8rem;
      color: var(--muted);
      text-transform: uppercase;
      margin-bottom: 1rem;
    }
    .color-swatches {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
    }
    .swatch {
      width: 36px; height: 36px;
      border-radius: 50%;
      border: 2px solid transparent;
      transition: border-color 0.2s, transform 0.2s;
    }
    .swatch:hover { transform: scale(1.1); }
    .swatch.active { border-color: #fff; }
    
    .config-btn {
      display: flex;
      justify-content: space-between;
      width: 100%;
      background: var(--surface);
      border: 1px solid var(--border);
      color: var(--text);
      padding: 1rem;
      font-family: var(--font-body);
      font-size: 1rem;
      transition: border-color 0.2s;
    }
    .config-btn:hover, .config-btn.active {
      border-color: var(--primary);
    }
    .config-btn .price { color: var(--muted); }
    .live-price-box {
      margin-top: auto;
      padding-top: 2rem;
      border-top: 1px solid var(--border);
    }
    .live-price {
      font-size: 3.5rem;
      color: var(--gold);
    }

    .testimonials-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5px;
      background: var(--border);
      border: 1px solid var(--border);
    }
    .test-card {
      background: var(--surface);
      padding: 3rem;
      border-left: 2px solid transparent;
      transition: border-color 0.3s;
    }
    .test-card:hover { border-left-color: var(--primary); }
    .quote-mark {
      font-family: var(--font-display);
      font-size: 4rem;
      color: var(--primary);
      line-height: 0.5;
      margin-bottom: 1rem;
    }
    .test-quote {
      font-size: 1.1rem;
      font-style: italic;
      color: var(--text);
      margin-bottom: 2rem;
      line-height: 1.6;
    }
    .test-author {
      display: flex;
      align-items: center;
      gap: 1rem;
    }
    .avatar {
      width: 40px; height: 40px;
      border-radius: 50%;
      background: var(--mid);
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-display);
      font-size: 1.2rem;
      color: var(--gold);
      border: 1px solid var(--border);
    }
    .author-info h4 { font-size: 1.2rem; margin-bottom: 0.2rem; }
    .author-info p { font-size: 0.8rem; color: var(--muted); }

    #waitlist {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      position: relative;
    }
    .waitlist-glow {
      position: absolute;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      width: 800px; height: 400px;
      background: radial-gradient(ellipse, rgba(232,41,11,0.15) 0%, transparent 70%);
      pointer-events: none;
      z-index: 0;
    }
    .waitlist-content {
      position: relative;
      z-index: 1;
      max-width: 600px;
    }
    .waitlist-divider {
      width: 60px; height: 1px;
      background: var(--primary);
      margin: 2rem auto;
    }
    .email-form {
      display: flex;
      border: 1px solid var(--border);
      margin-top: 3rem;
      background: var(--surface);
    }
    .email-input {
      flex: 1;
      background: transparent;
      border: none;
      padding: 1.2rem 1.5rem;
      color: var(--text);
      font-family: var(--font-body);
      font-size: 1.1rem;
      outline: none;
    }
    .email-btn {
      background: var(--primary);
      color: #fff;
      border: none;
      padding: 0 2rem;
      font-family: var(--font-display);
      font-size: 1.2rem;
      letter-spacing: 1px;
      clip-path: polygon(10px 0%, 100% 0%, 100% 100%, 0% 100%);
      transition: background 0.3s;
    }
    .email-btn:hover { background: #ff3a1a; }

    footer {
      background: #050505;
      border-top: 1px solid var(--border);
      padding: 4rem 10vw;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .footer-links {
      display: flex;
      gap: 2rem;
    }
    .footer-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.9rem;
      transition: color 0.3s;
    }
    .footer-links a:hover { color: var(--primary); }
    .copyright {
      color: var(--muted);
      font-family: var(--font-mono);
      font-size: 0.8rem;
    }

    .reveal {
      opacity: 0;
      transform: translateY(40px);
      transition: opacity 0.8s ease-out, transform 0.8s ease-out;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    @media (max-width: 1024px) {
      .specs-layout, .config-layout { grid-template-columns: 1fr; }
      .models-grid, .features-grid, .testimonials-grid { grid-template-columns: repeat(2, 1fr); }
    }
    @media (max-width: 768px) {
      .models-grid, .features-grid, .testimonials-grid { grid-template-columns: 1fr; }
      nav { padding: 1.5rem; }
      .nav-links { display: none; }
      section { padding: 5rem 1.5rem; }
      .hero-stats { bottom: 1.5rem; right: 1.5rem; gap: 1.5rem; }
      .stat-item h3 { font-size: 2rem; }
    }
  </style>
</head>
<body>

  <div id="loader">
    <div class="logo-loader">APEX</div>
    <div class="progress-wrapper">
      <div class="progress-bar" id="loader-bar"></div>
    </div>
  </div>

  <div id="cursor"></div>
  <div id="cursor-ring"></div>

  <nav id="navbar">
    <a href="#" class="nav-logo">APE<span class="text-red">X</span></a>
    <div class="nav-links">
      <a href="#models">Models</a>
      <a href="#specs">Performance</a>
      <a href="#experience">Experience</a>
      <a href="#configurator">Configure</a>
    </div>
    <a href="#configurator" class="btn-red" style="padding: 0.6rem 1.5rem; font-size: 0.9rem;">Book a Test Drive</a>
  </nav>

  <section id="hero">
    <div id="hero-canvas"></div>
    <div class="hero-content">
      <div class="hero-badge reveal">NEW 2025 LINEUP</div>
      <h1 class="hero-h1 bebas reveal">BORN / FROM / <span class="text-red">SPEED</span></h1>
      <p class="hero-sub reveal">Where aerodynamic precision meets unbridled power. Experience the apex of automotive engineering, crafted for those who demand absolute performance without compromise.</p>
      <div class="hero-ctas reveal">
        <a href="#models" class="btn-red">Explore Models</a>
        <a href="#configurator" class="ghost-link">Configure Yours</a>
      </div>
    </div>
    <div class="scroll-indicator">
      <div class="scroll-line"></div>
      <span class="scroll-text">SCROLL</span>
    </div>
    <div class="hero-stats">
      <div class="stat-item reveal">
        <h3 class="bebas">1050<span class="text-red">HP</span></h3>
        <p>Power</p>
      </div>
      <div class="stat-item reveal">
        <h3 class="bebas">2.7<span class="text-red">S</span></h3>
        <p>0-60 MPH</p>
      </div>
      <div class="stat-item reveal">
        <h3 class="bebas">220<span class="text-red">+</span></h3>
        <p>TOP SPEED</p>
      </div>
    </div>
  </section>

  <div id="marquee">
    <div class="marquee-track">
      <span class="marquee-item">Carbon Fibre Monocoque</span>
      <span class="marquee-item">Twin-Turbo V12</span>
      <span class="marquee-item">Active Aerodynamics</span>
      <span class="marquee-item">Launch Control System</span>
      <span class="marquee-item">Ceramic Composite Brakes</span>
      <span class="marquee-item">Hybrid Powerunit</span>
      <span class="marquee-item">F1-Derived Technology</span>
      
      <span class="marquee-item">Carbon Fibre Monocoque</span>
      <span class="marquee-item">Twin-Turbo V12</span>
      <span class="marquee-item">Active Aerodynamics</span>
      <span class="marquee-item">Launch Control System</span>
      <span class="marquee-item">Ceramic Composite Brakes</span>
      <span class="marquee-item">Hybrid Powerunit</span>
      <span class="marquee-item">F1-Derived Technology</span>
    </div>
  </div>

  <section id="models">
    <div class="section-header">
      <div>
        <span class="section-tag reveal">Series 1</span>
        <h2 class="section-title bebas reveal">THE LINEUP</h2>
      </div>
      <a href="#" class="ghost-link reveal">View All Models</a>
    </div>
    
    <div class="models-grid reveal">
      <div class="model-card" data-color="#e8290b">
        <div class="model-canvas-wrapper"></div>
        <div class="model-badge">$2.4M</div>
        <div class="model-info">
          <span class="model-type">TRACK</span>
          <h3 class="model-name bebas">APEX GTR</h3>
          <span class="model-specs">1050HP · 2.7s · 800KG DF</span>
        </div>
      </div>
      <div class="model-card" data-color="#d4a017">
        <div class="model-canvas-wrapper"></div>
        <div class="model-badge">$890K</div>
        <div class="model-info">
          <span class="model-type">GRAND TOURING</span>
          <h3 class="model-name bebas">APEX GT</h3>
          <span class="model-specs">800HP · 3.1s · V8 HYBRID</span>
        </div>
      </div>
      <div class="model-card" data-color="#0088cc">
        <div class="model-canvas-wrapper"></div>
        <div class="model-badge">$1.8M</div>
        <div class="model-info">
          <span class="model-type">ELECTRIC</span>
          <h3 class="model-name bebas">APEX EV-R</h3>
          <span class="model-specs">1400HP · 1.9s · AWD</span>
        </div>
      </div>
    </div>
  </section>

  <section id="specs">
    <div class="specs-layout">
      <div class="specs-content">
        <span class="section-tag reveal">Engineering</span>
        <h2 class="section-title bebas reveal">RAW NUMBERS</h2>
        <p class="specs-desc reveal">Forged in the wind tunnel and perfected on the track. The APEX powertrain delivers relentless acceleration and unshakeable stability at limit-pushing speeds.</p>
        
        <div class="specs-list">
          <div class="spec-item reveal">
            <span class="spec-label">Engine</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="100%"></div></div>
            <div class="spec-val bebas">7.0L <span class="spec-unit">V12</span></div>
          </div>
          <div class="spec-item reveal">
            <span class="spec-label">Power</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="100%"></div></div>
            <div class="spec-val bebas">1050 <span class="spec-unit">HP</span></div>
          </div>
          <div class="spec-item reveal">
            <span class="spec-label">Torque</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="88%"></div></div>
            <div class="spec-val bebas">900 <span class="spec-unit">NM</span></div>
          </div>
          <div class="spec-item reveal">
            <span class="spec-label">0-60 MPH</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="98%"></div></div>
            <div class="spec-val bebas">2.7 <span class="spec-unit">S</span></div>
          </div>
          <div class="spec-item reveal">
            <span class="spec-label">Top Speed</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="85%"></div></div>
            <div class="spec-val bebas">220 <span class="spec-unit">MPH</span></div>
          </div>
          <div class="spec-item reveal">
            <span class="spec-label">Downforce</span>
            <div class="spec-bar-bg"><div class="spec-bar-fill" data-width="90%"></div></div>
            <div class="spec-val bebas">800 <span class="spec-unit">KG</span></div>
          </div>
        </div>
      </div>
      
      <div class="engine-canvas-wrapper reveal" id="engine-canvas"></div>
    </div>
  </section>

  <section id="experience">
    <span class="section-tag reveal">Lifestyle</span>
    <h2 class="section-title bebas reveal">OWNERSHIP EXPERIENCE</h2>
    <p class="hero-sub reveal" style="margin: 1rem auto;">Joining the APEX family means access to a world of uncompromising luxury and motorsport heritage.</p>
    
    <div class="features-grid reveal">
      <div class="feature-cell">
        <span class="feature-icon">🏁</span>
        <h3 class="feature-title bebas">Track Days</h3>
        <p class="feature-desc">Private circuit access around the globe with professional racing instructors.</p>
      </div>
      <div class="feature-cell">
        <span class="feature-icon">🔧</span>
        <h3 class="feature-title bebas">Concierge Service</h3>
        <p class="feature-desc">24/7 flying technicians ready to service your vehicle anywhere in the world.</p>
      </div>
      <div class="feature-cell">
        <span class="feature-icon">✈️</span>
        <h3 class="feature-title bebas">Global Delivery</h3>
        <p class="feature-desc">White-glove delivery service to any location, securely transported.</p>
      </div>
      <div class="feature-cell">
        <span class="feature-icon">🏆</span>
        <h3 class="feature-title bebas">Owners Club</h3>
        <p class="feature-desc">Exclusive invitations to private rallies, unveiling events, and galas.</p>
      </div>
    </div>
  </section>

  <section id="configurator">
    <span class="section-tag reveal">Bespoke</span>
    <h2 class="section-title bebas reveal">BUILD YOUR APEX</h2>
    
    <div class="config-layout">
      <div class="config-canvas-wrapper reveal" id="config-canvas"></div>
      
      <div class="config-options reveal">
        
        <div class="config-group">
          <div class="config-group-title">Exterior Color</div>
          <div class="color-swatches">
            <div class="swatch active" style="background:#e8290b" data-color="#e8290b"></div>
            <div class="swatch" style="background:#0a0a0a" data-color="#0a0a0a"></div>
            <div class="swatch" style="background:#c0c0c0" data-color="#c0c0c0"></div>
            <div class="swatch" style="background:#d4a017" data-color="#d4a017"></div>
            <div class="swatch" style="background:#1a2b4c" data-color="#1a2b4c"></div>
            <div class="swatch" style="background:#f0f0f0" data-color="#f0f0f0"></div>
          </div>
        </div>

        <div class="config-group">
          <div class="config-group-title">Interior Trim</div>
          <button class="config-btn active" data-price="0"><span>Carbon Fibre</span> <span class="price">Included</span></button>
          <button class="config-btn" data-price="15000"><span>Alcantara</span> <span class="price">+$15,000</span></button>
          <button class="config-btn" data-price="22000"><span>Full Leather</span> <span class="price">+$22,000</span></button>
          <button class="config-btn" data-price="35000"><span>Bespoke</span> <span class="price">+$35,000</span></button>
        </div>

        <div class="config-group">
          <div class="config-group-title">Performance Pack</div>
          <button class="config-btn active" data-price="0"><span>Standard</span> <span class="price">Included</span></button>
          <button class="config-btn" data-price="45000"><span>Track Pack</span> <span class="price">+$45,000</span></button>
          <button class="config-btn" data-price="95000"><span>Race Edition</span> <span class="price">+$95,000</span></button>
        </div>
        
        <div class="config-group">
          <div class="config-group-title">Wheels</div>
          <button class="config-btn active" data-price="0"><span>20" Forged</span> <span class="price">Included</span></button>
          <button class="config-btn" data-price="12000"><span>21" Carbon</span> <span class="price">+$12,000</span></button>
          <button class="config-btn" data-price="28000"><span>22" Titanium</span> <span class="price">+$28,000</span></button>
        </div>

        <div class="live-price-box">
          <div class="config-group-title">Estimated Total</div>
          <div class="live-price bebas" id="total-price">$890,000</div>
        </div>
        
      </div>
    </div>
  </section>

  <section id="testimonials">
    <span class="section-tag reveal">Legacy</span>
    <h2 class="section-title bebas reveal">DRIVERS SPEAK</h2>
    
    <div class="testimonials-grid reveal">
      <div class="test-card">
        <div class="quote-mark">"</div>
        <p class="test-quote">The aerodynamic grip is unlike anything I've experienced. It feels planted at speeds that would unsettle even dedicated race cars. Pure adrenaline.</p>
        <div class="test-author">
          <div class="avatar" style="color: #e8290b;">AS</div>
          <div class="author-info">
            <h4 class="bebas">Alessandro Sforza</h4>
            <p>Milan, Italy</p>
          </div>
        </div>
      </div>
      <div class="test-card">
        <div class="quote-mark">"</div>
        <p class="test-quote">A masterpiece of engineering. The V12 symphony combined with the immediate torque of the hybrid system makes every drive an occasion.</p>
        <div class="test-author">
          <div class="avatar" style="color: #d4a017;">RK</div>
          <div class="author-info">
            <h4 class="bebas">Ravi Krishnamurti</h4>
            <p>Singapore</p>
          </div>
        </div>
      </div>
      <div class="test-card">
        <div class="quote-mark">"</div>
        <p class="test-quote">From the bespoke interior to the aggressive stance, APEX doesn't just build cars; they craft automotive art. It's the crown jewel of my collection.</p>
        <div class="test-author">
          <div class="avatar" style="color: #0088cc;">NB</div>
          <div class="author-info">
            <h4 class="bebas">Natasha Beaumont</h4>
            <p>London, UK</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="waitlist">
    <div class="waitlist-glow"></div>
    <div class="waitlist-content reveal">
      <h2 class="section-title bebas" style="font-size: 5rem;">ONLY 47 UNITS<br>AVAILABLE WORLDWIDE</h2>
      <div class="waitlist-divider"></div>
      <p class="hero-sub" style="margin: 0 auto;">Production is strictly limited to ensure exclusivity. Secure your allocation today.</p>
      <form class="email-form" onsubmit="event.preventDefault();">
        <input type="email" class="email-input" placeholder="Enter your email address..." required>
        <button type="submit" class="email-btn">APPLY NOW</button>
      </form>
    </div>
  </section>

  <footer>
    <div class="nav-logo">APE<span class="text-red">X</span></div>
    <div class="footer-links">
      <a href="#">Privacy</a>
      <a href="#">Terms</a>
      <a href="#">Media</a>
      <a href="#">Careers</a>
      <a href="#">Contact</a>
    </div>
    <div class="copyright">© 2025 APEX AUTOMOTIVE. ALL RIGHTS RESERVED.</div>
  </footer>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/ScrollTrigger.min.js"></script>

  <script>
    gsap.registerPlugin(ScrollTrigger);

    const cursor = document.getElementById('cursor');
    const cursorRing = document.getElementById('cursor-ring');
    let mouseX = 0, mouseY = 0;
    let ringX = 0, ringY = 0;

    document.addEventListener('mousemove', (e) => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      cursor.style.left = mouseX + 'px';
      cursor.style.top = mouseY + 'px';
    });

    gsap.ticker.add(() => {
      ringX += (mouseX - ringX) * 0.2;
      ringY += (mouseY - ringY) * 0.2;
      cursorRing.style.left = ringX + 'px';
      cursorRing.style.top = ringY + 'px';
    });

    const interactables = document.querySelectorAll('a, button, .swatch, input');
    interactables.forEach(el => {
      el.addEventListener('mouseenter', () => {
        cursor.style.width = '24px';
        cursor.style.height = '24px';
        cursorRing.style.width = '60px';
        cursorRing.style.height = '60px';
      });
      el.addEventListener('mouseleave', () => {
        cursor.style.width = '12px';
        cursor.style.height = '12px';
        cursorRing.style.width = '36px';
        cursorRing.style.height = '36px';
      });
    });

    let progress = 0;
    const loaderBar = document.getElementById('loader-bar');
    const loader = document.getElementById('loader');
    
    const loadInt = setInterval(() => {
      progress += Math.random() * 15;
      if (progress > 100) progress = 100;
      loaderBar.style.width = progress + '%';
      
      if (progress === 100) {
        clearInterval(loadInt);
        setTimeout(() => {
          loader.style.opacity = '0';
          loader.style.transform = 'translateY(-20px)';
          setTimeout(() => {
            loader.style.display = 'none';
            initScrollReveals();
          }, 500);
        }, 300);
      }
    }, 200);

    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      if (window.scrollY > 80) {
        navbar.classList.add('scrolled');
      } else {
        navbar.classList.remove('scrolled');
      }
    });

    function initScrollReveals() {
      const reveals = document.querySelectorAll('.reveal');
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible');
            
            if (entry.target.classList.contains('spec-item')) {
              entry.target.classList.add('active');
              const fill = entry.target.querySelector('.spec-bar-fill');
              if (fill) {
                fill.style.width = fill.getAttribute('data-width');
              }
            }
          }
        });
      }, { threshold: 0.1 });

      reveals.forEach(el => observer.observe(el));
    }

    function createCarGeometry() {
      const carGroup = new THREE.Group();
      
      const bodyMat = new THREE.MeshStandardMaterial({ 
        color: 0xe8290b, metalness: 0.9, roughness: 0.12 
      });
      const glassMat = new THREE.MeshStandardMaterial({ 
        color: 0x050505, metalness: 0.9, roughness: 0.1, transparent: true, opacity: 0.85 
      });
      const darkMat = new THREE.MeshStandardMaterial({ color: 0x111111, roughness: 0.8 });
      const silverMat = new THREE.MeshStandardMaterial({ color: 0x888888, metalness: 0.8, roughness: 0.2 });

      const body = new THREE.Mesh(new THREE.BoxGeometry(3.5, 0.45, 1.6), bodyMat);
      body.position.y = 0.225;
      carGroup.add(body);

      const cabin = new THREE.Mesh(new THREE.BoxGeometry(1.3, 0.38, 1.3), glassMat);
      cabin.position.set(-0.2, 0.64, 0);
      carGroup.add(cabin);

      const splitter = new THREE.Mesh(new THREE.BoxGeometry(2.2, 0.04, 0.3), darkMat);
      splitter.position.set(1.5, 0.02, 0);
      carGroup.add(splitter);

      const wingBlade = new THREE.Mesh(new THREE.BoxGeometry(2.0, 0.06, 0.18), darkMat);
      wingBlade.position.set(-1.6, 0.7, 0);
      carGroup.add(wingBlade);
      
      const pillar1 = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.25, 0.05), darkMat);
      pillar1.position.set(-1.6, 0.57, 0.4);
      carGroup.add(pillar1);
      
      const pillar2 = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.25, 0.05), darkMat);
      pillar2.position.set(-1.6, 0.57, -0.4);
      carGroup.add(pillar2);

      const wheelPos = [
        [1.1, 0.2, 0.85], [1.1, 0.2, -0.85], 
        [-1.1, 0.2, 0.85], [-1.1, 0.2, -0.85]
      ];
      
      wheelPos.forEach(pos => {
        const wheel = new THREE.Group();
        
        const tire = new THREE.Mesh(new THREE.CylinderGeometry(0.3, 0.3, 0.2, 32), darkMat);
        tire.rotation.x = Math.PI / 2;
        wheel.add(tire);
        
        const rim = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.2, 0.22, 16), silverMat);
        rim.rotation.x = Math.PI / 2;
        wheel.add(rim);
        
        wheel.position.set(...pos);
        carGroup.add(wheel);
      });

      return { group: carGroup, bodyMat };
    }

    const heroContainer = document.getElementById('hero-canvas');
    const heroScene = new THREE.Scene();
    heroScene.background = new THREE.Color(0x090909);
    
    const heroCamera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 100);
    heroCamera.position.set(0, 0, 5);
    
    const heroRenderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
    heroRenderer.setSize(window.innerWidth, window.innerHeight);
    heroRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    heroRenderer.shadowMap.enabled = true;
    heroRenderer.shadowMap.type = THREE.PCFSoftShadowMap;
    heroContainer.appendChild(heroRenderer.domElement);

    heroScene.add(new THREE.AmbientLight(0xffffff, 0.15));
    
    const dirLight = new THREE.DirectionalLight(0xfff0e0, 2.5);
    dirLight.position.set(5, 8, 5);
    dirLight.castShadow = true;
    heroScene.add(dirLight);

    const heroRedLight = new THREE.PointLight(0xe8290b, 3, 20);
    heroRedLight.position.set(-4, 0, 3);
    heroScene.add(heroRedLight);

    const rimLight = new THREE.DirectionalLight(0x4488ff, 1.2);
    rimLight.position.set(-5, 2, -5);
    heroScene.add(rimLight);

    heroScene.add(new THREE.HemisphereLight(0x001133, 0x110000, 0.5));

    const { group: heroCar } = createCarGeometry();
    heroCar.position.set(1.8, -0.05, 0);
    heroCar.rotation.y = -0.35;
    
    heroCar.traverse(child => {
      if(child.isMesh) {
        child.castShadow = true;
        child.receiveShadow = true;
      }
    });
    heroScene.add(heroCar);

    const groundMat = new THREE.MeshStandardMaterial({ color: 0x050505, roughness: 0.8 });
    const ground = new THREE.Mesh(new THREE.PlaneGeometry(30, 30), groundMat);
    ground.rotation.x = -Math.PI / 2;
    ground.position.y = -0.6;
    ground.receiveShadow = true;
    heroScene.add(ground);

    const grid = new THREE.GridHelper(30, 40, 0xe8290b, 0x111111);
    grid.position.y = -0.59;
    grid.material.opacity = 0.2;
    grid.material.transparent = true;
    heroScene.add(grid);

    const partGeo = new THREE.BufferGeometry();
    const partCnt = 200;
    const partPos = new Float32Array(partCnt * 3);
    for(let i=0; i<partCnt*3; i++) {
      partPos[i] = (Math.random() - 0.5) * 20;
    }
    partGeo.setAttribute('position', new THREE.BufferAttribute(partPos, 3));
    const partMat = new THREE.PointsMaterial({
      size: 0.04, color: 0xe8290b, transparent: true, opacity: 0.4
    });
    const particles = new THREE.Points(partGeo, partMat);
    heroScene.add(particles);

    let pX = 0, pY = 0;
    document.addEventListener('mousemove', (e) => {
      pX = (e.clientX / window.innerWidth - 0.5) * 2;
      pY = (e.clientY / window.innerHeight - 0.5) * 2;
    });

    const clock = new THREE.Clock();

    function renderHero() {
      const t = clock.getElapsedTime();
      
      heroCar.position.y = -0.05 + Math.sin(t) * 0.03;
      heroCar.rotation.y = -0.35 + Math.sin(t * 0.5) * 0.06;
      heroCar.rotation.x = pY * -0.04;
      
      heroRedLight.intensity = 2 + Math.sin(t * 2) * 1;
      particles.rotation.y = t * 0.05;
      
      heroRenderer.render(heroScene, heroCamera);
    }

    const modelCards = document.querySelectorAll('.model-card');
    const modelRenderers = [];
    
    modelCards.forEach(card => {
      const wrapper = card.querySelector('.model-canvas-wrapper');
      const color = parseInt(card.dataset.color.replace('#', '0x'));
      
      const mScene = new THREE.Scene();
      const mCam = new THREE.PerspectiveCamera(50, wrapper.clientWidth / wrapper.clientHeight, 0.1, 20);
      mCam.position.set(0, 1.5, 4.5);
      mCam.lookAt(0, 0, 0);
      
      const mRenderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
      mRenderer.setSize(wrapper.clientWidth, wrapper.clientHeight);
      mRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      wrapper.appendChild(mRenderer.domElement);
      
      mScene.add(new THREE.AmbientLight(0xffffff, 0.4));
      const mDir = new THREE.DirectionalLight(0xffffff, 1);
      mDir.position.set(2, 4, 3);
      mScene.add(mDir);
      
      const mPoint = new THREE.PointLight(color, 5, 10);
      mPoint.position.set(-2, 1, 2);
      mScene.add(mPoint);
      
      const { group: mCar, bodyMat: mMat } = createCarGeometry();
      mMat.color.setHex(color);
      mCar.scale.set(0.6, 0.6, 0.6);
      mCar.rotation.y = 0.4;
      mScene.add(mCar);
      
      const mGrid = new THREE.GridHelper(10, 20, 0x333333, 0x111111);
      mGrid.position.y = -0.3;
      mScene.add(mGrid);
      
      card.addEventListener('mouseenter', () => {
        gsap.to(mCar.rotation, { y: 0.2, duration: 0.5, ease: "power2.out" });
      })# Business Requirements Document (BRD)
## Corporate Expense & Budget Management Dashboard

### 1. Executive Summary
The organization currently relies on manual spreadsheets to track departmental expenses against allocated budgets. This manual process causes a 2-week delay in reporting, resulting in budget overruns and missed opportunities for cost optimization. The proposed project is an automated **Corporate Expense & Budget Management Dashboard** that provides real-time visibility into financial health.

### 2. Project Objectives
- **Automate Data Consolidation**: Reduce manual data entry by aggregating data from the ERP system.
- **Real-Time Visibility**: Provide executives and department heads with an up-to-date view of budget vs. actuals.
- **Anomaly Detection**: Highlight excessive spending or unusual transactions automatically.

### 3. Scope
**In-Scope:**
- Dashboard showing Total Budget, Total Spend, Remaining Budget, and Burn Rate.
- Visual breakdown of expenses by Department and Category (e.g., Travel, Software, Payroll).
- Export functionality for reports.

**Out-of-Scope:**
- Payroll processing or invoice payment capabilities.
- Predictive forecasting (slated for Phase 2).

### 4. Stakeholders
- **Chief Financial Officer (CFO)**: Executive Sponsor.
- **FP&A Team**: Primary users.
- **Department Heads**: End users for budget tracking.
- **IT Department**: Data integration and security.

### 5. Functional Requirements
- **FR-01**: The system must securely authenticate users based on their active directory roles.
- **FR-02**: The dashboard must display total aggregated metrics (Spend, Budget, Variance) at the top of the page.
- **FR-03**: The user must be able to filter data by Date Range and Department.
- **FR-04**: The system must highlight any department exceeding 90% of their allocated budget in red.

### 6. Non-Functional Requirements
- **Performance**: The dashboard must load within 3 seconds.
- **Security**: Financial data must be encrypted at rest and in transit.

      card.addEventListener('mouseleave', () => {
        gsap.to(mCar.rotation, { y: 0.4, duration: 0.5, ease: "power2.out" });
      });

      modelRenderers.push({ scene: mScene, camera: mCam, renderer: mRenderer, car: mCar, wrapper: wrapper });
    });

    function renderModels() {
      const t = clock.getElapsedTime();
      modelRenderers.forEach(obj => {
        obj.car.position.y = Math.sin(t * 2) * 0.02;
        obj.renderer.render(obj.scene, obj.camera);
      });
    }

    const engineWrapper = document.getElementById('engine-canvas');
    const eScene = new THREE.Scene();
    const eCam = new THREE.PerspectiveCamera(45, 1, 0.1, 20);
    eCam.position.set(4, 3, 5);
    eCam.lookAt(0, 0, 0);
    
    const eRenderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    eRenderer.setSize(engineWrapper.clientWidth, engineWrapper.clientHeight);
    eRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    engineWrapper.appendChild(eRenderer.domElement);

    eScene.add(new THREE.AmbientLight(0xffffff, 0.3));
    const eDir = new THREE.DirectionalLight(0xffffff, 1.5);
    eDir.position.set(5, 5, 2);
    eScene.add(eDir);

    const ePoint = new THREE.PointLight(0xe8290b, 5, 10);
    eScene.add(ePoint);

    const engineGroup = new THREE.Group();
    
    const blockMat = new THREE.MeshStandardMaterial({ color: 0xaaaaaa, metalness: 0.8, roughness: 0.3 });
    const block = new THREE.Mesh(new THREE.BoxGeometry(1.5, 1, 2), blockMat);
    engineGroup.add(block);

    const cylMat = new THREE.MeshStandardMaterial({ color: 0x888888, metalness: 0.9, roughness: 0.2 });
    const darkDiscMat = new THREE.MeshStandardMaterial({ color: 0x111111 });
    
    for(let i=0; i<4; i++) {
      const cyl = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.16, 0.5, 16), cylMat);
      cyl.position.set(0, 0.75, -0.6 + i*0.4);
      engineGroup.add(cyl);
      
      const head = new THREE.Mesh(new THREE.CylinderGeometry(0.17, 0.17, 0.05, 16), darkDiscMat);
      head.position.set(0, 1.0, -0.6 + i*0.4);
      engineGroup.add(head);
    }

    const crankMat = new THREE.MeshStandardMaterial({ color: 0xe8290b, metalness: 0.7, roughness: 0.2 });
    const crank = new THREE.Mesh(new THREE.CylinderGeometry(0.08, 0.08, 2.4, 12), crankMat);
    crank.rotation.x = Math.PI/2;
    crank.position.y = -0.5;
    engineGroup.add(crank);

    const ringMat1 = new THREE.MeshBasicMaterial({ color: 0xe8290b });
    const ringMat2 = new THREE.MeshBasicMaterial({ color: 0x4488ff });
    const ringMat3 = new THREE.MeshBasicMaterial({ color: 0xffffff });
    
    const ring1 = new THREE.Mesh(new THREE.TorusGeometry(2.2, 0.02, 16, 100), ringMat1);
    const ring2 = new THREE.Mesh(new THREE.TorusGeometry(2.7, 0.02, 16, 100), ringMat2);
    const ring3 = new THREE.Mesh(new THREE.TorusGeometry(3.1, 0.02, 16, 100), ringMat3);
    
    ring1.rotation.x = 1.2;
    ring2.rotation.y = 1.5;
    ring3.rotation.x = -0.5;
    ring3.rotation.y = 0.8;
    
    eScene.add(ring1);
    eScene.add(ring2);
    eScene.add(ring3);

    eScene.add(engineGroup);

    function renderEngine() {
      const t = clock.getElapsedTime();
      
      ePoint.position.x = Math.cos(t) * 3;
      ePoint.position.z = Math.sin(t) * 3;
      ePoint.position.y = 1;
      
      engineGroup.rotation.y = t * 0.2;
      engineGroup.rotation.x = Math.sin(t * 0.5) * 0.1;
      
      ring1.rotation.z = t * 1.5;
      ring2.rotation.z = -t * 1.2;
      ring3.rotation.z = t * 0.8;
      
      eRenderer.render(eScene, eCam);
    }

    const configWrapper = document.getElementById('config-canvas');
    const cScene = new THREE.Scene();
    const cCam = new THREE.PerspectiveCamera(45, configWrapper.clientWidth / configWrapper.clientHeight, 0.1, 20);
    cCam.position.set(0, 0.8, 5);
    
    const cRenderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    cRenderer.setSize(configWrapper.clientWidth, configWrapper.clientHeight);
    cRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    configWrapper.appendChild(cRenderer.domElement);

    cScene.add(new THREE.AmbientLight(0xffffff, 0.6));
    const cDir = new THREE.DirectionalLight(0xffffff, 1.5);
    cDir.position.set(3, 5, 4);
    cScene.add(cDir);
    
    const cFill = new THREE.DirectionalLight(0xffffff, 0.5);
    cFill.position.set(-3, 2, -4);
    cScene.add(cFill);

    const { group: configCar, bodyMat: configMat } = createCarGeometry();
    configCar.scale.set(0.8, 0.8, 0.8);
    cScene.add(configCar);

    let isDragging = false;
    let previousMousePosition = { x: 0 };
    let targetRot = 0;

    configWrapper.addEventListener('mousedown', (e) => {
      isDragging = true;
      previousMousePosition = { x: e.offsetX };
    });
    window.addEventListener('mouseup', () => { isDragging = false; });
    window.addEventListener('mousemove', (e) => {
      if (isDragging) {
        const deltaMove = e.offsetX - previousMousePosition.x;
        targetRot += deltaMove * 0.01;
        previousMousePosition = { x: e.offsetX };
      }
    });

    configWrapper.addEventListener('touchstart', (e) => {
      isDragging = true;
      previousMousePosition = { x: e.touches[0].clientX };
    }, {passive: true});
    window.addEventListener('touchend', () => { isDragging = false; });
    window.addEventListener('touchmove', (e) => {
      if(isDragging) {
        const deltaMove = e.touches[0].clientX - previousMousePosition.x;
        targetRot += deltaMove * 0.01;
        previousMousePosition = { x: e.touches[0].clientX };
      }
    }, {passive: true});


    function renderConfig() {
      configCar.rotation.y += (targetRot - configCar.rotation.y) * 0.1;
      cRenderer.render(cScene, cCam);
    }

    const basePrice = 890000;
    let configState = { interior: 0, performance: 0, wheels: 0 };
    const priceDisplay = document.getElementById('total-price');
    
    function updatePrice() {
      const total = basePrice + configState.interior + configState.performance + configState.wheels;
      priceDisplay.innerText = '$' + total.toLocaleString();
    }

    document.querySelectorAll('.swatch').forEach(swatch => {
      swatch.addEventListener('click', (e) => {
        document.querySelectorAll('.swatch').forEach(s => s.classList.remove('active'));
        e.target.classList.add('active');
        const color = parseInt(e.target.dataset.color.replace('#', '0x'));
        configMat.color.setHex(color);
      });
    });

    document.querySelectorAll('.config-group').forEach((group, index) => {
      if(index === 0) return; 
      
      const buttons = group.querySelectorAll('.config-btn');
      let type = '';
      if(index === 1) type = 'interior';
      if(index === 2) type = 'performance';
      if(index === 3) type = 'wheels';

      buttons.forEach(btn => {
        btn.addEventListener('click', (e) => {
          buttons.forEach(b => b.classList.remove('active'));
          const target = e.target.closest('.config-btn');
          target.classList.add('active');
          configState[type] = parseInt(target.dataset.price);
          updatePrice();
        });
      });
    });

    function animate() {
      requestAnimationFrame(animate);
      renderHero();
      renderModels();
      renderEngine();
      renderConfig();
    }
    animate();

    window.addEventListener('resize', () => {
      heroCamera.aspect = window.innerWidth / window.innerHeight;
      heroCamera.updateProjectionMatrix();
      heroRenderer.setSize(window.innerWidth, window.innerHeight);

      modelRenderers.forEach(obj => {
        obj.camera.aspect = obj.wrapper.clientWidth / obj.wrapper.clientHeight;
        obj.camera.updateProjectionMatrix();
        obj.renderer.setSize(obj.wrapper.clientWidth, obj.wrapper.clientHeight);
      });

      eCam.aspect = engineWrapper.clientWidth / engineWrapper.clientHeight;
      eCam.updateProjectionMatrix();
      eRenderer.setSize(engineWrapper.clientWidth, engineWrapper.clientHeight);

      cCam.aspect = configWrapper.clientWidth / configWrapper.clientHeight;
      cCam.updateProjectionMatrix();
      cRenderer.setSize(configWrapper.clientWidth, configWrapper.clientHeight);
    });

  </script>
</body>
</html>
