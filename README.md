<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Skyline Digital — Design Studio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0B0E14;
    --surface:#13171F;
    --card:#171C26;
    --line:rgba(245,243,239,0.08);
    --text:#F5F3EF;
    --muted:#8B95A5;
    --accent:#FF5C39;
    --accent2:#7C3AED;
    --r-lg:18px;
    --r-md:10px;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg);
    color:var(--text);
    font-family:'Inter',sans-serif;
    overflow-x:hidden;
  }
  .mono{font-family:'JetBrains Mono',monospace;}
  .display{font-family:'Space Grotesk',sans-serif;}

  /* ===== NAV ===== */
  nav{
    position:fixed;top:0;left:0;right:0;z-index:100;
    display:flex;align-items:center;justify-content:space-between;
    padding:22px 6vw;
    backdrop-filter:blur(14px);
    background:rgba(11,14,20,0.55);
    border-bottom:1px solid var(--line);
    transition:padding .3s ease;
  }
  .logo{
    font-family:'Space Grotesk',sans-serif;
    font-weight:700;
    font-size:20px;
    letter-spacing:0.5px;
    display:flex;align-items:center;gap:10px;
  }
  .logo-mark{
    width:28px;height:28px;border-radius:6px;
    background:linear-gradient(135deg,var(--accent),var(--accent2));
    display:flex;align-items:center;justify-content:center;
    font-size:14px;font-weight:700;color:#0B0E14;
  }
  .nav-links{display:flex;gap:36px;align-items:center;}
  .nav-links a{
    color:var(--muted);text-decoration:none;font-size:14px;font-weight:500;
    transition:color .25s ease;letter-spacing:0.2px;
  }
  .nav-links a:hover{color:var(--text);}
  .nav-cta{
    background:var(--text);color:var(--bg);
    padding:10px 22px;border-radius:100px;
    font-size:14px;font-weight:600;text-decoration:none;
    transition:transform .25s ease, box-shadow .25s ease;
  }
  .nav-cta:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(255,92,57,0.25);}
  .nav-toggle{display:none;background:none;border:none;color:var(--text);font-size:24px;cursor:pointer;}

  /* ===== HERO ===== */
  .hero{
    min-height:100vh;
    display:flex;flex-direction:column;justify-content:center;
    padding:0 6vw;
    position:relative;
    background:
      radial-gradient(ellipse 60% 50% at 50% -10%, rgba(124,58,237,0.18), transparent 60%),
      radial-gradient(ellipse 50% 40% at 80% 110%, rgba(255,92,57,0.12), transparent 60%);
  }
  .hero-eyebrow{
    font-family:'JetBrains Mono',monospace;
    color:var(--accent);
    font-size:13px;letter-spacing:3px;text-transform:uppercase;
    margin-bottom:24px;
    display:flex;align-items:center;gap:12px;
    opacity:0;animation:fadeUp 0.8s ease forwards;
    animation-delay:0.1s;
  }
  .hero-eyebrow::before{
    content:'';width:36px;height:1px;background:var(--accent);
  }
  .hero h1{
    font-family:'Space Grotesk',sans-serif;
    font-weight:700;
    font-size:clamp(48px,9vw,118px);
    line-height:0.98;
    letter-spacing:-2px;
    max-width:1200px;
    opacity:0;animation:fadeUp 0.9s ease forwards;
    animation-delay:0.25s;
  }
  .hero h1 .grad{
    background:linear-gradient(120deg,var(--accent),var(--accent2));
    -webkit-background-clip:text;background-clip:text;color:transparent;
  }
  .hero p{
    margin-top:28px;
    max-width:560px;
    font-size:18px;line-height:1.7;color:var(--muted);
    opacity:0;animation:fadeUp 0.9s ease forwards;
    animation-delay:0.4s;
  }
  .hero-actions{
    margin-top:44px;display:flex;gap:18px;flex-wrap:wrap;
    opacity:0;animation:fadeUp 0.9s ease forwards;
    animation-delay:0.55s;
  }
  .btn-primary{
    background:var(--accent);color:#fff;
    padding:16px 34px;border-radius:100px;
    font-weight:600;font-size:15px;text-decoration:none;
    box-shadow:0 0 0 0 rgba(255,92,57,0.4);
    transition:transform .25s ease, box-shadow .25s ease;
  }
  .btn-primary:hover{transform:translateY(-3px);box-shadow:0 12px 32px rgba(255,92,57,0.35);}
  .btn-secondary{
    border:1px solid var(--line);color:var(--text);
    padding:16px 34px;border-radius:100px;
    font-weight:600;font-size:15px;text-decoration:none;
    transition:border-color .25s ease, background .25s ease;
  }
  .btn-secondary:hover{border-color:var(--text);background:var(--surface);}

  @keyframes fadeUp{
    from{opacity:0;transform:translateY(24px);}
    to{opacity:1;transform:translateY(0);}
  }

  /* ===== SKYLINE SIGNATURE ===== */
  .skyline-bar{
    margin-top:80px;
    display:grid;
    grid-template-columns:repeat(5,1fr);
    gap:2px;
    border-top:1px solid var(--line);
    opacity:0;animation:fadeUp 1s ease forwards;
    animation-delay:0.7s;
  }
  .building{
    position:relative;
    border-right:1px solid var(--line);
    padding:28px 24px 20px;
    cursor:pointer;
    overflow:hidden;
    transition:background .35s ease, padding-top .35s ease;
    text-decoration:none;color:var(--text);
  }
  .building:last-child{border-right:none;}
  .building::before{
    content:'';position:absolute;inset:0;
    background:linear-gradient(180deg,transparent,rgba(255,92,57,0.06));
    opacity:0;transition:opacity .35s ease;
  }
  .building:hover::before{opacity:1;}
  .building:hover{padding-top:44px;background:var(--surface);}
  .b-num{
    font-family:'JetBrains Mono',monospace;
    font-size:12px;color:var(--accent);letter-spacing:2px;
  }
  .b-name{
    font-family:'Space Grotesk',sans-serif;
    font-weight:700;font-size:clamp(20px,3vw,32px);
    margin-top:60px;letter-spacing:-0.5px;
  }
  .b-windows{
    display:grid;grid-template-columns:repeat(6,1fr);gap:4px;
    margin-top:18px;
  }
  .b-windows span{
    aspect-ratio:1;border-radius:2px;
    background:rgba(245,243,239,0.06);
    transition:background .4s ease;
  }
  .building:hover .b-windows span{background:rgba(255,92,57,0.35);}
  .building:hover .b-windows span:nth-child(3n){background:rgba(124,58,237,0.4);}

  /* ===== SECTIONS GENERAL ===== */
  section{padding:140px 6vw;}
  .section-head{
    display:flex;justify-content:space-between;align-items:flex-end;
    margin-bottom:70px;flex-wrap:wrap;gap:24px;
  }
  .section-tag{
    font-family:'JetBrains Mono',monospace;color:var(--accent);
    font-size:13px;letter-spacing:3px;text-transform:uppercase;
    margin-bottom:14px;display:block;
  }
  .section-head h2{
    font-family:'Space Grotesk',sans-serif;font-weight:700;
    font-size:clamp(32px,5vw,56px);letter-spacing:-1.5px;
  }
  .section-head p{color:var(--muted);max-width:380px;font-size:15px;line-height:1.7;}

  /* ===== WORK GRID / GALLERY ===== */
  .filters{display:flex;gap:10px;margin-bottom:48px;flex-wrap:wrap;}
  .filter-btn{
    font-family:'JetBrains Mono',monospace;font-size:13px;
    padding:10px 20px;border-radius:100px;border:1px solid var(--line);
    background:transparent;color:var(--muted);cursor:pointer;
    transition:all .25s ease;letter-spacing:1px;
  }
  .filter-btn.active, .filter-btn:hover{
    color:var(--bg);background:var(--text);border-color:var(--text);
  }
  .grid{
    display:grid;grid-template-columns:repeat(3,1fr);gap:24px;
  }
  .work-card{
    border-radius:var(--r-lg);overflow:hidden;
    background:var(--card);border:1px solid var(--line);
    cursor:pointer;position:relative;
    transition:transform .4s cubic-bezier(.16,1,.3,1), border-color .4s ease;
  }
  .work-card:hover{transform:translateY(-8px);border-color:rgba(255,92,57,0.4);}
  .work-thumb{
    width:100%;aspect-ratio:4/3;object-fit:cover;display:block;
    background:linear-gradient(135deg,#1A1F2B,#0B0E14);
  }
  .work-thumb.placeholder{
    display:flex;align-items:center;justify-content:center;
    color:var(--muted);font-family:'JetBrains Mono',monospace;font-size:13px;
    flex-direction:column;gap:10px;
  }
  .work-thumb.placeholder svg{opacity:0.3;}
  .work-info{padding:20px 22px;}
  .work-cat{
    font-family:'JetBrains Mono',monospace;color:var(--accent);
    font-size:11px;letter-spacing:2px;text-transform:uppercase;
  }
  .work-title{
    font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:19px;
    margin-top:8px;letter-spacing:-0.3px;
  }
  .work-remove{
    position:absolute;top:14px;right:14px;
    width:32px;height:32px;border-radius:50%;
    background:rgba(11,14,20,0.7);backdrop-filter:blur(6px);
    border:1px solid var(--line);color:var(--text);
    display:flex;align-items:center;justify-content:center;
    cursor:pointer;font-size:16px;opacity:0;
    transition:opacity .25s ease, background .25s ease;
    z-index:2;
  }
  .work-card:hover .work-remove{opacity:1;}
  .work-remove:hover{background:rgba(255,92,57,0.85);}

  /* upload card */
  .upload-card{
    border:1px dashed var(--line);border-radius:var(--r-lg);
    display:flex;flex-direction:column;align-items:center;justify-content:center;
    gap:14px;aspect-ratio:4/3;cursor:pointer;text-align:center;
    transition:border-color .3s ease, background .3s ease;
    color:var(--muted);
  }
  .upload-card:hover{border-color:var(--accent);background:var(--surface);color:var(--text);}
  .upload-card svg{opacity:0.6;}
  .upload-card span{font-size:13px;font-family:'JetBrains Mono',monospace;letter-spacing:1px;}
  .upload-card.full{
    grid-column:1/-1;aspect-ratio:auto;padding:60px 20px;
  }

  /* ===== ABOUT / PROCESS ===== */
  .about-grid{
    display:grid;grid-template-columns:1.1fr 1fr;gap:80px;align-items:start;
  }
  .about-text p{
    font-size:18px;line-height:1.85;color:var(--muted);margin-bottom:24px;
  }
  .about-text p strong{color:var(--text);font-weight:600;}
  .stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--line);border-radius:var(--r-lg);overflow:hidden;}
  .stat{background:var(--card);padding:36px 28px;}
  .stat-num{
    font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:42px;
    background:linear-gradient(120deg,var(--accent),var(--accent2));
    -webkit-background-clip:text;background-clip:text;color:transparent;
  }
  .stat-label{margin-top:8px;color:var(--muted);font-size:13px;letter-spacing:0.5px;}

  /* ===== SERVICES ===== */
  .services{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;}
  .service-card{
    background:var(--card);border:1px solid var(--line);border-radius:var(--r-lg);
    padding:36px 30px;transition:border-color .3s ease, transform .3s ease;
  }
  .service-card:hover{border-color:rgba(255,92,57,0.35);transform:translateY(-6px);}
  .service-icon{
    width:46px;height:46px;border-radius:12px;
    background:linear-gradient(135deg,rgba(255,92,57,0.18),rgba(124,58,237,0.18));
    display:flex;align-items:center;justify-content:center;margin-bottom:24px;
  }
  .service-card h3{
    font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:21px;
    margin-bottom:12px;letter-spacing:-0.3px;
  }
  .service-card p{color:var(--muted);font-size:14px;line-height:1.7;}

  /* ===== PROCESS TIMELINE ===== */
  .process{display:grid;grid-template-columns:repeat(4,1fr);gap:0;border-top:1px solid var(--line);}
  .process-step{
    padding:36px 24px;border-right:1px solid var(--line);position:relative;
  }
  .process-step:last-child{border-right:none;}
  .process-num{
    font-family:'JetBrains Mono',monospace;color:var(--accent);font-size:13px;
    letter-spacing:2px;margin-bottom:60px;display:block;
  }
  .process-step h4{
    font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:19px;margin-bottom:10px;
  }
  .process-step p{color:var(--muted);font-size:14px;line-height:1.65;}

  /* ===== CONTACT / CTA ===== */
  .cta-section{
    text-align:center;position:relative;
    background:radial-gradient(ellipse 60% 60% at 50% 50%, rgba(255,92,57,0.1), transparent 70%);
  }
  .cta-section h2{
    font-family:'Space Grotesk',sans-serif;font-weight:700;
    font-size:clamp(38px,7vw,84px);letter-spacing:-2px;line-height:1.05;
    margin-bottom:30px;
  }
  .cta-section p{color:var(--muted);font-size:18px;max-width:520px;margin:0 auto 44px;line-height:1.7;}
  .contact-row{display:flex;gap:18px;justify-content:center;flex-wrap:wrap;}

  /* ===== FOOTER ===== */
  footer{
    border-top:1px solid var(--line);padding:50px 6vw;
    display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:20px;
  }
  footer .logo{font-size:16px;}
  .footer-links{display:flex;gap:30px;}
  .footer-links a{color:var(--muted);text-decoration:none;font-size:14px;transition:color .25s ease;}
  .footer-links a:hover{color:var(--text);}
  .footer-copy{color:var(--muted);font-size:13px;font-family:'JetBrains Mono',monospace;}

  /* ===== LIGHTBOX ===== */
  .lightbox{
    position:fixed;inset:0;background:rgba(11,14,20,0.92);backdrop-filter:blur(10px);
    z-index:1000;display:none;align-items:center;justify-content:center;
    padding:40px;flex-direction:column;
  }
  .lightbox.active{display:flex;}
  .lightbox-content{
    max-width:min(900px,90vw);width:100%;
    background:var(--card);border:1px solid var(--line);border-radius:var(--r-lg);
    overflow:hidden;
    animation:lbIn .35s cubic-bezier(.16,1,.3,1);
  }
  @keyframes lbIn{from{opacity:0;transform:scale(0.96) translateY(20px);}to{opacity:1;transform:scale(1) translateY(0);}}
  .lightbox-img{width:100%;max-height:60vh;object-fit:contain;background:#05070B;display:block;}
  .lightbox-body{padding:28px 32px;}
  .lightbox-close{
    position:absolute;top:28px;right:28px;
    width:44px;height:44px;border-radius:50%;
    background:var(--card);border:1px solid var(--line);color:var(--text);
    display:flex;align-items:center;justify-content:center;font-size:20px;cursor:pointer;
    transition:background .25s ease;
  }
  .lightbox-close:hover{background:var(--accent);}

  /* ===== SCROLL REVEAL ===== */
  .reveal{opacity:0;transform:translateY(36px);transition:opacity .8s cubic-bezier(.16,1,.3,1), transform .8s cubic-bezier(.16,1,.3,1);}
  .reveal.visible{opacity:1;transform:translateY(0);}

  /* ===== RESPONSIVE ===== */
  @media (max-width:900px){
    .nav-links{display:none;}
    .nav-toggle{display:block;}
    .grid{grid-template-columns:repeat(2,1fr);}
    .skyline-bar{grid-template-columns:repeat(2,1fr);}
    .building:nth-child(2),.building:nth-child(4){border-right:none;}
    .about-grid{grid-template-columns:1fr;gap:50px;}
    .services{grid-template-columns:1fr;}
    .process{grid-template-columns:1fr;}
    .process-step{border-right:none;border-bottom:1px solid var(--line);}
  }
  @media (max-width:560px){
    .grid{grid-template-columns:1fr;}
    section{padding:90px 6vw;}
    .hero h1{font-size:14vw;}
  }
</style>
</head>
<body>

<nav>
  <div class="logo"><div class="logo-mark">SD</div>Skyline Digital</div>
  <div class="nav-links">
    <a href="#work">Work</a>
    <a href="#services">Services</a>
    <a href="#about">About</a>
    <a href="#process">Process</a>
    <a href="#contact" class="nav-cta">Start a project</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero" style="padding-top:120px;">
  <div class="hero-eyebrow">Graphic design studio — Karachi, Pakistan</div>
  <h1>We design the<br>visuals your brand<br><span class="grad">can't go without.</span></h1>
  <p>Skyline Digital crafts logos, social banners, stream overlays and full brand kits engineered to make scrolling stop and clients hit "send".</p>
  <div class="hero-actions">
    <a href="#contact" class="btn-primary">Get a quote</a>
    <a href="#work" class="btn-secondary">View work</a>
  </div>

  <div class="skyline-bar">
    <a href="#work" class="building" data-filter="logo">
      <span class="b-num">01 / IDENTITY</span>
      <div class="b-name">Logos</div>
      <div class="b-windows"><span></span><span></span><span></span><span></span><span></span><span></span></div>
    </a>
    <a href="#work" class="building" data-filter="banner">
      <span class="b-num">02 / SOCIAL</span>
      <div class="b-name">Banners</div>
      <div class="b-windows"><span></span><span></span><span></span><span></span><span></span><span></span></div>
    </a>
    <a href="#work" class="building" data-filter="overlay">
      <span class="b-num">03 / STREAM</span>
      <div class="b-name">Overlays</div>
      <div class="b-windows"><span></span><span></span><span></span><span></span><span></span><span></span></div>
    </a>
    <a href="#work" class="building" data-filter="branding">
      <span class="b-num">04 / SYSTEM</span>
      <div class="b-name">Branding</div>
      <div class="b-windows"><span></span><span></span><span></span><span></span><span></span><span></span></div>
    </a>
    <a href="#work" class="building" data-filter="website">
      <span class="b-num">05 / WEB</span>
      <div class="b-name">Websites</div>
      <div class="b-windows"><span></span><span></span><span></span><span></span><span></span><span></span></div>
    </a>
  </div>
</section>

<!-- WORK -->
<section id="work">
  <div class="section-head reveal">
    <div>
      <span class="section-tag">Selected work</span>
      <h2>Portfolio</h2>
    </div>
    <p>Every piece below is a real deliverable. Add your own designs — they'll appear instantly in the grid.</p>
  </div>

  <div class="filters reveal">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="logo">Logos</button>
    <button class="filter-btn" data-filter="banner">Banners</button>
    <button class="filter-btn" data-filter="overlay">Overlays</button>
    <button class="filter-btn" data-filter="branding">Branding</button>
    <button class="filter-btn" data-filter="website">Websites</button>
  </div>

  <div class="grid reveal" id="workGrid">
    <!-- Sample placeholder items -->
    <div class="work-card" data-cat="logo" data-title="Nova Athletics — Logo mark" data-cat-label="Logo design">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#2A1F3D);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="12" r="9"/><path d="M12 3v18M3 12h18"/></svg>
        <span>SAMPLE — LOGO</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Logo design</span>
        <div class="work-title">Nova Athletics — Logo mark</div>
      </div>
    </div>

    <div class="work-card" data-cat="banner" data-title="Drift Records — Spotify canvas" data-cat-label="Social banner">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#3D2418);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="M3 9h18"/></svg>
        <span>SAMPLE — BANNER</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Social banner</span>
        <div class="work-title">Drift Records — Spotify canvas</div>
      </div>
    </div>

    <div class="work-card" data-cat="overlay" data-title="Pixel Forge — Stream overlay kit" data-cat-label="Stream overlay">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#1C2E3D);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="M2 16l4-4 4 4 6-6 4 4"/></svg>
        <span>SAMPLE — OVERLAY</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Stream overlay</span>
        <div class="work-title">Pixel Forge — Stream overlay kit</div>
      </div>
    </div>

    <div class="work-card" data-cat="branding" data-title="Halcyon Coffee — Brand system" data-cat-label="Branding">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#2A3322);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M3 6h18M3 12h18M3 18h18"/></svg>
        <span>SAMPLE — BRANDING</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Branding</span>
        <div class="work-title">Halcyon Coffee — Brand system</div>
      </div>
    </div>

    <div class="work-card" data-cat="logo" data-title="Orbital — Wordmark + icon" data-cat-label="Logo design">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#2A1F3D);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="12" r="9"/><path d="M12 3v18M3 12h18"/></svg>
        <span>SAMPLE — LOGO</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Logo design</span>
        <div class="work-title">Orbital — Wordmark + icon</div>
      </div>
    </div>

    <div class="work-card" data-cat="website" data-title="Skyline Digital — Portfolio site" data-cat-label="Website design">
      <div class="work-thumb placeholder" style="background:linear-gradient(135deg,#1A1F2B,#1C2436);">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="3" width="20" height="18" rx="2"/><path d="M2 8h20M6 5.5h.01M9 5.5h.01"/></svg>
        <span>SAMPLE — WEBSITE</span>
      </div>
      <div class="work-info">
        <span class="work-cat">Website design</span>
        <div class="work-title">Skyline Digital — Portfolio site</div>
      </div>
    </div>

    <!-- Upload card -->
    <div class="upload-card" id="uploadCard">
      <svg width="34" height="34" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 16V4M12 4l-4 4M12 4l4 4M4 16v2a2 2 0 002 2h12a2 2 0 002-2v-2"/></svg>
      <span>ADD YOUR DESIGN</span>
    </div>
    <input type="file" id="fileInput" accept="image/*" multiple style="display:none;">
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-grid">
    <div class="reveal">
      <span class="section-tag">About the studio</span>
      <div class="about-text">
        <p><strong>Skyline Digital</strong> is a one-person design studio building visual identities for brands, creators and businesses that refuse to look ordinary.</p>
        <p>From a single logo mark to a complete brand kit — every project gets the same obsession with detail: clean typography, deliberate color, and layouts that hold up at any size, on any screen.</p>
        <p>Clients come for one design. They stay because the next one's always better.</p>
      </div>
    </div>
    <div class="reveal">
      <div class="stat-grid">
        <div class="stat"><div class="stat-num">120+</div><div class="stat-label">PROJECTS DELIVERED</div></div>
        <div class="stat"><div class="stat-num">48h</div><div class="stat-label">AVG. TURNAROUND</div></div>
        <div class="stat"><div class="stat-num">35+</div><div class="stat-label">BRANDS BUILT</div></div>
        <div class="stat"><div class="stat-num">5.0</div><div class="stat-label">CLIENT RATING</div></div>
      </div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services">
  <div class="section-head reveal">
    <div>
      <span class="section-tag">What we build</span>
      <h2>Services</h2>
    </div>
    <p>Pick a single piece or a full system — everything is designed to work together.</p>
  </div>
  <div class="services reveal">
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><circle cx="12" cy="12" r="9"/><path d="M12 3v18M3 12h18"/></svg></div>
      <h3>Logo design</h3>
      <p>Wordmarks, icons and combination logos with full vector files, color variants and usage guidelines.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="M8 21h8M12 17v4"/></svg></div>
      <h3>Social banners</h3>
      <p>YouTube, Twitter/X, LinkedIn and Spotify cover art sized and optimized for every platform.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="M2 16l4-4 4 4 6-6 4 4"/></svg></div>
      <h3>Stream overlays</h3>
      <p>Twitch and YouTube overlay packs — alerts, panels, webcam frames and animated transitions.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><path d="M4 6h16M4 12h16M4 18h10"/></svg></div>
      <h3>Brand kits</h3>
      <p>Color palettes, type systems, business cards and social templates that keep a brand consistent.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><path d="M12 3v6m0 6v6M5 12h14"/></svg></div>
      <h3>Thumbnails</h3>
      <p>High-CTR YouTube thumbnails with bold type, color grading and composition built for the grid.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><rect x="4" y="4" width="16" height="16" rx="2"/><path d="M4 9h16M9 4v16"/></svg></div>
      <h3>Print & packaging</h3>
      <p>Posters, flyers, business cards and packaging mockups, print-ready in CMYK.</p>
    </div>
    <div class="service-card">
      <div class="service-icon"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#FF5C39" stroke-width="1.5"><rect x="2" y="3" width="20" height="18" rx="2"/><path d="M2 8h20M6 5.5h.01M9 5.5h.01"/></svg></div>
      <h3>Website design</h3>
      <p>Portfolio sites, landing pages and full custom websites — designed and built to convert.</p>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section id="process">
  <div class="section-head reveal">
    <div>
      <span class="section-tag">How it works</span>
      <h2>Process</h2>
    </div>
    <p>Simple, fast, and built around your feedback at every stage.</p>
  </div>
  <div class="process reveal">
    <div class="process-step">
      <span class="process-num">01</span>
      <h4>Brief</h4>
      <p>You send your idea, references and brand details — as detailed or rough as you like.</p>
    </div>
    <div class="process-step">
      <span class="process-num">02</span>
      <h4>Concepts</h4>
      <p>You receive 2–3 initial directions to react to within 24–48 hours.</p>
    </div>
    <div class="process-step">
      <span class="process-num">03</span>
      <h4>Refine</h4>
      <p>We lock the chosen direction and refine colors, type and layout based on your notes.</p>
    </div>
    <div class="process-step">
      <span class="process-num">04</span>
      <h4>Delivery</h4>
      <p>Final files delivered in every format you need — source files included.</p>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact" class="cta-section">
  <span class="section-tag reveal">Let's build something</span>
  <h2 class="reveal">Ready to make<br>your brand look<br>this good?</h2>
  <p class="reveal">Send your project details and reference images — you'll get a quote and timeline back within a day.</p>
  <div class="contact-row reveal">
    <a href="mailto:skylinedigital0305@gmail.com" class="btn-primary">skylinedigital0305@gmail.com</a>
  </div>
  <div class="contact-row reveal" style="margin-top:20px;">
    <a href="https://wa.me/923173951868" target="_blank" class="btn-secondary" style="display:flex;align-items:center;gap:10px;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M17.5 14.4c-.3-.1-1.7-.8-2-.9-.3-.1-.5-.1-.6.1-.2.3-.7.9-.9 1.1-.2.2-.3.2-.6.1-1.6-.8-2.7-1.4-3.8-3.2-.3-.5.3-.5.8-1.5.1-.2 0-.4-.1-.5-.1-.1-.6-1.5-.9-2-.2-.5-.4-.4-.6-.4-.2 0-.5 0-.7 0-.2 0-.6.1-.9.4-.3.3-1.2 1.2-1.2 2.8 0 1.7 1.2 3.3 1.4 3.5.1.2 2 3.2 5 4.3 2.4.9 2.9.7 3.5.6.6-.1 1.7-.7 1.9-1.4.3-.7.3-1.3.2-1.4-.1-.1-.2-.2-.5-.3zM12 2C6.5 2 2 6.5 2 12c0 1.9.5 3.7 1.5 5.3L2 22l4.8-1.5C8.4 21.5 10.2 22 12 22c5.5 0 10-4.5 10-10S17.5 2 12 2z"/></svg>
      WhatsApp — Fakhir Sheikh
    </a>
    <a href="https://wa.me/923143834773" target="_blank" class="btn-secondary" style="display:flex;align-items:center;gap:10px;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M17.5 14.4c-.3-.1-1.7-.8-2-.9-.3-.1-.5-.1-.6.1-.2.3-.7.9-.9 1.1-.2.2-.3.2-.6.1-1.6-.8-2.7-1.4-3.8-3.2-.3-.5.3-.5.8-1.5.1-.2 0-.4-.1-.5-.1-.1-.6-1.5-.9-2-.2-.5-.4-.4-.6-.4-.2 0-.5 0-.7 0-.2 0-.6.1-.9.4-.3.3-1.2 1.2-1.2 2.8 0 1.7 1.2 3.3 1.4 3.5.1.2 2 3.2 5 4.3 2.4.9 2.9.7 3.5.6.6-.1 1.7-.7 1.9-1.4.3-.7.3-1.3.2-1.4-.1-.1-.2-.2-.5-.3zM12 2C6.5 2 2 6.5 2 12c0 1.9.5 3.7 1.5 5.3L2 22l4.8-1.5C8.4 21.5 10.2 22 12 22c5.5 0 10-4.5 10-10S17.5 2 12 2z"/></svg>
      WhatsApp — Ali Sheikh
    </a>
  </div>
</section>

<footer>
  <div class="logo"><div class="logo-mark">SD</div>Skyline Digital</div>
  <div class="footer-links">
    <a href="#work">Work</a>
    <a href="#services">Services</a>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
  </div>
  <div class="footer-copy">© 2026 SKYLINE DIGITAL</div>
</footer>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox">
  <div class="lightbox-close" id="lightboxClose">&times;</div>
  <div class="lightbox-content">
    <img class="lightbox-img" id="lightboxImg" src="" alt="">
    <div class="lightbox-body">
      <span class="work-cat" id="lightboxCat"></span>
      <div class="work-title" id="lightboxTitle" style="margin-top:8px;"></div>
    </div>
  </div>
</div>

<script>
  // ===== Scroll reveal =====
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{ if(e.isIntersecting){ e.target.classList.add('visible'); } });
  },{threshold:0.15});
  reveals.forEach(el=>observer.observe(el));

  // ===== Filters =====
  const filterBtns = document.querySelectorAll('.filter-btn');
  const cards = ()=>document.querySelectorAll('#workGrid .work-card');
  function applyFilter(val){
    cards().forEach(c=>{
      c.style.display = (val==='all' || c.dataset.cat===val) ? '' : 'none';
    });
  }
  filterBtns.forEach(btn=>{
    btn.addEventListener('click',()=>{
      filterBtns.forEach(b=>b.classList.remove('active'));
      btn.classList.add('active');
      applyFilter(btn.dataset.filter);
    });
  });
  // skyline shortcuts jump + pre-filter
  document.querySelectorAll('.building').forEach(b=>{
    b.addEventListener('click',()=>{
      const target = b.dataset.filter;
      setTimeout(()=>{
        filterBtns.forEach(btn=>{
          if(btn.dataset.filter===target){ btn.click(); }
        });
      },400);
    });
  });

  // ===== Upload =====
  const uploadCard = document.getElementById('uploadCard');
  const fileInput = document.getElementById('fileInput');
  const grid = document.getElementById('workGrid');

  const catLabels = {
    logo:'Logo design',
    banner:'Social banner',
    overlay:'Stream overlay',
    branding:'Branding',
    website:'Website design'
  };

  uploadCard.addEventListener('click',()=>fileInput.click());

  fileInput.addEventListener('change',(e)=>{
    const files = Array.from(e.target.files);
    files.forEach(file=>{
      const reader = new FileReader();
      reader.onload = (ev)=>{
        addWorkCard(ev.target.result, file.name, 'logo');
      };
      reader.readAsDataURL(file);
    });
    fileInput.value='';
  });

  // drag & drop
  ['dragover','dragleave','drop'].forEach(evt=>{
    uploadCard.addEventListener(evt,(e)=>{
      e.preventDefault();
      if(evt==='dragover') uploadCard.style.borderColor='#FF5C39';
      if(evt==='dragleave') uploadCard.style.borderColor='';
      if(evt==='drop'){
        uploadCard.style.borderColor='';
        const files = Array.from(e.dataTransfer.files).filter(f=>f.type.startsWith('image/'));
        files.forEach(file=>{
          const reader = new FileReader();
          reader.onload = (ev)=>addWorkCard(ev.target.result, file.name, 'logo');
          reader.readAsDataURL(file);
        });
      }
    });
  });

  function addWorkCard(src, name, cat){
    const card = document.createElement('div');
    card.className='work-card';
    card.dataset.cat = cat;
    const title = name.replace(/\.[^/.]+$/,'');
    card.innerHTML = `
      <div class="work-remove" title="Remove">&times;</div>
      <img class="work-thumb" src="${src}" alt="${title}">
      <div class="work-info">
        <select class="work-cat-select mono" style="background:transparent;border:none;color:#FF5C39;font-size:11px;letter-spacing:2px;text-transform:uppercase;font-family:'JetBrains Mono',monospace;cursor:pointer;padding:0;">
          <option value="logo">Logo design</option>
          <option value="banner">Social banner</option>
          <option value="overlay">Stream overlay</option>
          <option value="branding">Branding</option>
          <option value="website">Website design</option>
        </select>
        <div class="work-title">${title}</div>
      </div>
    `;
    // insert before upload card
    grid.insertBefore(card, uploadCard);

    // remove
    card.querySelector('.work-remove').addEventListener('click',(e)=>{
      e.stopPropagation();
      card.remove();
    });

    // category select
    const select = card.querySelector('.work-cat-select');
    select.addEventListener('change',(e)=>{
      e.stopPropagation();
      card.dataset.cat = select.value;
      applyFilter(document.querySelector('.filter-btn.active').dataset.filter);
    });
    select.addEventListener('click', e=>e.stopPropagation());

    // lightbox openA
    card.addEventListener('click',(e)=>{
      if(e.target.tagName==='SELECT') return;
      openLightbox(src, title, catLabels[card.dataset.cat]);
    });

    applyFilter(document.querySelector('.filter-btn.active').dataset.filter);
  }

  // ===== Lightbox for sample (placeholder) cards =====
  document.querySelectorAll('#workGrid .work-card[data-cat]').forEach(card=>{
    if(card.querySelector('img')) return;
    card.addEventListener('click',()=>{
      const img = card.querySelector('.work-thumb');
      openLightbox(null, card.dataset.title, card.dataset.catLabel, img.style.background);
    });
  });

  function openLightbox(src, title, cat, bg){
    const lb = document.getElementById('lightbox');
    const lbImg = document.getElementById('lightboxImg');
    if(src){
      lbImg.src = src;
      lbImg.style.background='';
    } else {
      lbImg.removeAttribute('src');
      lbImg.style.background = bg || 'linear-gradient(135deg,#1A1F2B,#0B0E14)';
      lbImg.style.minHeight='320px';
    }
    document.getElementById('lightboxTitle').textContent = title;
    document.getElementById('lightboxCat').textContent = cat;
    lb.classList.add('active');
  }
  document.getElementById('lightboxClose').addEventListener('click',()=>{
    document.getElementById('lightbox').classList.remove('active');
  });
  document.getElementById('lightbox').addEventListener('click',(e)=>{
    if(e.target.id==='lightbox') e.currentTarget.classList.remove('active');
  });

  // ===== Mobile nav (simple) =====
  // keeps layout clean; nav-links hidden under 900px, anchors still work via scroll
</script>

</body>
</html>
