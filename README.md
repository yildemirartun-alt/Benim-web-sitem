# Benim-web-sitem
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VALORANT REHBER | Harita & Ajan Rehberi</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@400;600;700&family=Rajdhani:wght@400;500;600;700&family=Orbitron:wght@400;700&display=swap');

  :root {
    --red: #ff4454;
    --red-glow: rgba(255,68,84,0.35);
    --gold: #f5c842;
    --dark-bg: #0a0b0d;
    --card-bg: #111214;
    --card-border: #1e2026;
    --text: #c8ccd4;
    --text-bright: #eef0f4;
    --accent-blue: #00d4ff;
    --accent-green: #39ff8e;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  html { scroll-behavior:smooth; }

  body {
    background: var(--dark-bg);
    font-family: 'Rajdhani', sans-serif;
    color: var(--text);
    min-height:100vh;
    overflow-x:hidden;
  }

  /* ─── HERO ─── */
  .hero {
    position:relative;
    width:100%;
    height:100vh;
    min-height:500px;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    text-align:center;
    background: linear-gradient(180deg, #0a0b0d 0%, #0d1117 40%, #0a0b0d 100%);
    overflow:hidden;
  }
  .hero::before {
    content:'';
    position:absolute;
    inset:0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 30%, rgba(255,68,84,0.08) 0%, transparent 70%),
      radial-gradient(ellipse 60% 40% at 20% 80%, rgba(0,212,255,0.05) 0%, transparent 60%),
      radial-gradient(ellipse 50% 50% at 80% 70%, rgba(57,255,142,0.04) 0%, transparent 60%);
    pointer-events:none;
  }
  .hero-grid {
    position:absolute;
    inset:0;
    background-image:
      linear-gradient(rgba(255,68,84,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,68,84,0.03) 1px, transparent 1px);
    background-size:60px 60px;
    pointer-events:none;
    mask-image: radial-gradient(ellipse 70% 60% at 50% 50%, black 30%, transparent 70%);
    -webkit-mask-image: radial-gradient(ellipse 70% 60% at 50% 50%, black 30%, transparent 70%);
  }
  .hero-content { position:relative; z-index:2; padding:0 20px; }
  .hero-badge {
    display:inline-block;
    border:1px solid var(--red);
    color:var(--red);
    font-family:'Orbitron',sans-serif;
    font-size:11px;
    letter-spacing:3px;
    text-transform:uppercase;
    padding:6px 18px;
    margin-bottom:24px;
    border-radius:2px;
  }
  .hero h1 {
    font-family:'Orbitron',sans-serif;
    font-size:clamp(2.4rem,6vw,4.2rem);
    font-weight:700;
    color:#fff;
    line-height:1.1;
    letter-spacing:-1px;
  }
  .hero h1 span { color:var(--red); }
  .hero-sub {
    font-size:clamp(1rem,2vw,1.2rem);
    color:var(--text);
    margin-top:18px;
    max-width:600px;
    margin-left:auto;
    margin-right:auto;
    line-height:1.6;
    font-weight:500;
  }
  .hero-cta {
    margin-top:36px;
    display:flex;
    gap:14px;
    justify-content:center;
    flex-wrap:wrap;
  }
  .btn-primary {
    background:var(--red);
    color:#fff;
    border:none;
    padding:13px 32px;
    font-family:'Rajdhani',sans-serif;
    font-size:1rem;
    font-weight:700;
    letter-spacing:1.5px;
    text-transform:uppercase;
    cursor:pointer;
    text-decoration:none;
    border-radius:3px;
    transition: box-shadow .3s, transform .2s;
  }
  .btn-primary:hover { box-shadow:0 0 24px var(--red-glow); transform:translateY(-2px); }
  .btn-outline {
    background:transparent;
    color:var(--text-bright);
    border:1px solid var(--card-border);
    padding:13px 32px;
    font-family:'Rajdhani',sans-serif;
    font-size:1rem;
    font-weight:600;
    letter-spacing:1.5px;
    text-transform:uppercase;
    cursor:pointer;
    text-decoration:none;
    border-radius:3px;
    transition: border-color .3s, color .3s;
  }
  .btn-outline:hover { border-color:var(--red); color:var(--red); }

  /* ─── NAV ─── */
  nav {
    position:fixed;
    top:0; left:0; right:0;
    z-index:100;
    background:rgba(10,11,13,0.85);
    backdrop-filter:blur(12px);
    border-bottom:1px solid var(--card-border);
    padding:14px 0;
    transition:transform .3s;
  }
  .nav-inner {
    max-width:1200px;
    margin:0 auto;
    padding:0 24px;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }
  .nav-logo {
    font-family:'Orbitron',sans-serif;
    font-size:1rem;
    color:#fff;
    font-weight:700;
    letter-spacing:2px;
    text-decoration:none;
  }
  .nav-logo span { color:var(--red); }
  .nav-links { display:flex; gap:28px; list-style:none; }
  .nav-links a {
    color:var(--text);
    text-decoration:none;
    font-size:.85rem;
    font-weight:600;
    letter-spacing:1px;
    text-transform:uppercase;
    transition:color .2s;
  }
  .nav-links a:hover { color:var(--red); }

  /* ─── SECTION COMMON ─── */
  section { padding:80px 24px; }
  .section-inner { max-width:1200px; margin:0 auto; }
  .section-header { text-align:center; margin-bottom:56px; }
  .section-header h2 {
    font-family:'Oswald',sans-serif;
    font-size:clamp(1.8rem,4vw,2.6rem);
    color:#fff;
    font-weight:600;
    text-transform:uppercase;
    letter-spacing:2px;
  }
  .section-header h2 span { color:var(--red); }
  .section-header p { color:var(--text); margin-top:10px; font-size:1rem; font-weight:500; }
  .tag {
    display:inline-block;
    font-family:'Orbitron',sans-serif;
    font-size:9px;
    letter-spacing:2px;
    text-transform:uppercase;
    color:var(--red);
    margin-bottom:10px;
  }

  /* ─── META INFO BAR ─── */
  .meta-bar {
    background:var(--card-bg);
    border-top:1px solid var(--card-border);
    border-bottom:1px solid var(--card-border);
    padding:28px 24px;
  }
  .meta-bar-inner {
    max-width:1200px;
    margin:0 auto;
    display:flex;
    gap:40px;
    flex-wrap:wrap;
    justify-content:center;
  }
  .meta-stat {
    text-align:center;
    flex:1;
    min-width:140px;
  }
  .meta-stat .num {
    font-family:'Orbitron',sans-serif;
    font-size:2rem;
    font-weight:700;
    color:var(--red);
  }
  .meta-stat .label { font-size:.8rem; color:var(--text); letter-spacing:1px; text-transform:uppercase; margin-top:4px; }

  /* ─── ROLES SECTION ─── */
  .roles-grid {
    display:grid;
    grid-template-columns: repeat(auto-fit, minmax(240px,1fr));
    gap:18px;
  }
  .role-card {
    background:var(--card-bg);
    border:1px solid var(--card-border);
    border-radius:6px;
    padding:28px 22px;
    transition: border-color .3s, transform .2s;
  }
  .role-card:hover { border-color:var(--red); transform:translateY(-3px); }
  .role-icon { font-size:1.8rem; margin-bottom:12px; }
  .role-card h3 {
    font-family:'Oswald',sans-serif;
    font-size:1.1rem;
    color:#fff;
    text-transform:uppercase;
    letter-spacing:1px;
    margin-bottom:8px;
  }
  .role-card p { font-size:.88rem; line-height:1.5; color:var(--text); }
  .role-card .agents-list {
    margin-top:14px;
    display:flex;
    flex-wrap:wrap;
    gap:6px;
  }
  .agent-pill {
    background:rgba(255,68,84,0.1);
    border:1px solid rgba(255,68,84,0.25);
    color:var(--red);
    font-size:.75rem;
    font-weight:600;
    padding:3px 10px;
    border-radius:3px;
    letter-spacing:.5px;
  }

  /* ─── MAP FILTER ─── */
  .filter-bar {
    display:flex;
    gap:10px;
    flex-wrap:wrap;
    justify-content:center;
    margin-bottom:40px;
  }
  .filter-btn {
    background:transparent;
    border:1px solid var(--card-border);
    color:var(--text);
    padding:8px 18px;
    font-family:'Rajdhani',sans-serif;
    font-size:.85rem;
    font-weight:600;
    letter-spacing:1px;
    text-transform:uppercase;
    cursor:pointer;
    border-radius:3px;
    transition: all .25s;
  }
  .filter-btn:hover, .filter-btn.active {
    background:var(--red);
    border-color:var(--red);
    color:#fff;
  }

  /* ─── MAP CARDS ─── */
  .maps-grid {
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(340px,1fr));
    gap:20px;
  }
  .map-card {
    background:var(--card-bg);
    border:1px solid var(--card-border);
    border-radius:8px;
    overflow:hidden;
    transition: border-color .3s, transform .2s;
    cursor:pointer;
  }
  .map-card:hover { border-color:var(--red); transform:translateY(-4px); }
  .map-card-header {
    position:relative;
    padding:28px 24px 20px;
    background: linear-gradient(135deg, rgba(255,68,84,0.06) 0%, transparent 60%);
  }
  .map-status {
    position:absolute;
    top:16px; right:16px;
    font-size:.7rem;
    font-weight:700;
    letter-spacing:1.5px;
    text-transform:uppercase;
    padding:3px 10px;
    border-radius:3px;
  }
  .map-status.comp { background:rgba(57,255,142,0.12); color:var(--accent-green); border:1px solid rgba(57,255,142,0.25); }
  .map-status.casual { background:rgba(0,212,255,0.12); color:var(--accent-blue); border:1px solid rgba(0,212,255,0.25); }
  .map-card-header h3 {
    font-family:'Oswald',sans-serif;
    font-size:1.5rem;
    color:#fff;
    text-transform:uppercase;
    letter-spacing:2px;
  }
  .map-card-header .map-loc {
    font-size:.78rem;
    color:var(--text);
    margin-top:4px;
    letter-spacing:.5px;
  }
  .map-card-body { padding:0 24px 22px; }
  .map-desc { font-size:.88rem; color:var(--text); line-height:1.55; margin-bottom:16px; }
  .map-feature {
    display:flex;
    align-items:center;
    gap:8px;
    font-size:.78rem;
    color:var(--text);
    margin-bottom:6px;
  }
  .map-feature .dot {
    width:6px; height:6px;
    background:var(--red);
    border-radius:50%;
    flex-shrink:0;
  }
  .map-agents {
    margin-top:18px;
    padding-top:16px;
    border-top:1px solid var(--card-border);
  }
  .map-agents-label { font-size:.72rem; color:var(--text); letter-spacing:1px; text-transform:uppercase; margin-bottom:8px; }
  .map-agents .agents-row { display:flex; flex-wrap:wrap; gap:6px; }

  /* ─── TEAM COMP SECTION ─── */
  .comp-cards {
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(320px,1fr));
    gap:20px;
  }
  .comp-card {
    background:var(--card-bg);
    border:1px solid var(--card-border);
    border-radius:8px;
    padding:26px 22px;
    transition: border-color .3s;
  }
  .comp-card:hover { border-color:var(--gold); }
  .comp-card h3 {
    font-family:'Oswald',sans-serif;
    font-size:1.15rem;
    color:#fff;
    text-transform:uppercase;
    letter-spacing:1.5px;
    margin-bottom:6px;
  }
  .comp-card .comp-map { font-size:.75rem; color:var(--gold); letter-spacing:1px; text-transform:uppercase; margin-bottom:14px; }
  .comp-row {
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:10px;
  }
  .comp-role-tag {
    font-size:.65rem;
    font-weight:700;
    letter-spacing:1px;
    text-transform:uppercase;
    padding:3px 8px;
    border-radius:2px;
    min-width:72px;
    text-align:center;
    flex-shrink:0;
  }
  .comp-role-tag.duelist { background:rgba(255,68,84,0.15); color:var(--red); border:1px solid rgba(255,68,84,0.25); }
  .comp-role-tag.controller { background:rgba(0,212,255,0.12); color:var(--accent-blue); border:1px solid rgba(0,212,255,0.2); }
  .comp-role-tag.initiator { background:rgba(245,200,66,0.12); color:var(--gold); border:1px solid rgba(245,200,66,0.25); }
  .comp-role-tag.sentinel { background:rgba(57,255,142,0.12); color:var(--accent-green); border:1px solid rgba(57,255,142,0.2); }
  .comp-agent-name { font-size:.9rem; color:#fff; font-weight:600; }
  .comp-agent-desc { font-size:.78rem; color:var(--text); }

  /* ─── TIPS SECTION ─── */
  .tips-grid {
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(280px,1fr));
    gap:18px;
  }
  .tip-card {
    background:var(--card-bg);
    border:1px solid var(--card-border);
    border-radius:8px;
    padding:28px 22px;
    position:relative;
    overflow:hidden;
    transition: transform .2s;
  }
  .tip-card:hover { transform:translateY(-3px); }
  .tip-card::before {
    content:'';
    position:absolute;
    top:0; left:0; right:0;
    height:3px;
    background: linear-gradient(90deg, var(--red), var(--accent-blue));
  }
  .tip-num {
    font-family:'Orbitron',sans-serif;
    font-size:2rem;
    font-weight:700;
    color:rgba(255,68,84,0.15);
    line-height:1;
    margin-bottom:14px;
  }
  .tip-card h3 {
    font-family:'Oswald',sans-serif;
    font-size:1.05rem;
    color:#fff;
    text-transform:uppercase;
    letter-spacing:1px;
    margin-bottom:8px;
  }
  .tip-card p { font-size:.87rem; color:var(--text); line-height:1.6; }

  /* ─── TIER TABLE ─── */
  .tier-table { width:100%; border-radius:8px; overflow:hidden; border:1px solid var(--card-border); }
  .tier-row {
    display:flex;
    align-items:center;
    border-bottom:1px solid var(--card-border);
    min-height:60px;
  }
  .tier-row:last-child { border-bottom:none; }
  .tier-label {
    width:70px;
    min-width:70px;
    text-align:center;
    font-family:'Orbitron',sans-serif;
    font-size:1.1rem;
    font-weight:700;
    height:100%;
    display:flex;
    align-items:center;
    justify-content:center;
  }
  .tier-label.s { background:rgba(255,68,84,0.18); color:var(--red); }
  .tier-label.a { background:rgba(245,200,66,0.15); color:var(--gold); }
  .tier-label.b { background:rgba(0,212,255,0.12); color:var(--accent-blue); }
  .tier-agents {
    flex:1;
    display:flex;
    flex-wrap:wrap;
    gap:8px;
    padding:14px 18px;
    background:var(--card-bg);
  }
  .tier-agent {
    font-size:.82rem;
    font-weight:600;
    color:var(--text-bright);
    background:rgba(255,255,255,0.05);
    border:1px solid var(--card-border);
    padding:4px 12px;
    border-radius:3px;
  }

  /* ─── FOOTER ─── */
  footer {
    background:var(--card-bg);
    border-top:1px solid var(--card-border);
    text-align:center;
    padding:40px 24px;
  }
  footer p { font-size:.78rem; color:var(--text); letter-spacing:.5px; }
  footer .disclaimer { margin-top:8px; font-size:.7rem; color:#444; max-width:600px; margin-left:auto; margin-right:auto; line-height:1.5; }

  /* ─── RESPONSIVE ─── */
  @media(max-width:600px){
    .nav-links { display:none; }
    .maps-grid, .comp-cards { grid-template-columns:1fr; }
    .meta-bar-inner { gap:20px; }
    section { padding:60px 18px; }
  }

  /* ─── SCROLL REVEAL ─── */
  .reveal { opacity:0; transform:translateY(22px); transition:opacity .6s ease, transform .6s ease; }
  .reveal.visible { opacity:1; transform:translateY(0); }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-inner">
    <a href="#" class="nav-logo">VAL<span>REHBER</span></a>
    <ul class="nav-links">
      <li><a href="#roles">Roller</a></li>
      <li><a href="#maps">Haritalar</a></li>
      <li><a href="#comps">Takım Kurma</a></li>
      <li><a href="#tips">İpuçları</a></li>
      <li><a href="#tiers">Tier List</a></li>
    </ul>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-grid"></div>
  <div class="hero-content">
    <div class="hero-badge">2025 Güncel Meta Rehberi</div>
    <h1>VALORANT'A<br/><span>USTACA</span> BAŞLA</h1>
    <p class="hero-sub">Tüm 12 harita için en iyi ajanları, takım kurma stratejilerini ve profesyonel ipuçlarını öğren. Rankedde yüksel, oyuna egemen ol.</p>
    <div class="hero-cta">
      <a href="#maps" class="btn-primary">Haritaları Incela</a>
      <a href="#tips" class="btn-outline">Başlangıç İpuçları</a>
    </div>
  </div>
</section>

<!-- META BAR -->
<div class="meta-bar">
  <div class="meta-bar-inner">
    <div class="meta-stat"><div class="num">12</div><div class="label">Toplam Harita</div></div>
    <div class="meta-stat"><div class="num">7</div><div class="label">Kompetitif Havuz</div></div>
    <div class="meta-stat"><div class="num">28</div><div class="label">Toplam Ajan</div></div>
    <div class="meta-stat"><div class="num">4</div><div class="label">Ajan Rolü</div></div>
  </div>
</div>

<!-- ROLES -->
<section id="roles">
  <div class="section-inner">
    <div class="section-header reveal">
      <div class="tag">Temel Bilgiler</div>
      <h2>AJAN <span>ROLLERI</span></h2>
      <p>Her takımda 5 oyuncu var. Her birinin farklı bir rolü olmalı.</p>
    </div>
    <div class="roles-grid">
      <div class="role-card reveal">
        <div class="role-icon">⚔️</div>
        <h3>Duelist – Saldırgan</h3>
        <p>Takımın ana fragger'ı. Site almak için öne çıkar ve düşman öldürür. En agresif rol.</p>
        <div class="agents-list">
          <span class="agent-pill">Jett</span>
          <span class="agent-pill">Neon</span>
          <span class="agent-pill">Reyna</span>
          <span class="agent-pill">Raze</span>
          <span class="agent-pill">Phoenix</span>
          <span class="agent-pill">Clove</span>
        </div>
      </div>
      <div class="role-card reveal">
        <div class="role-icon">🛡️</div>
        <h3>Sentinel – Savunucu</h3>
        <p>Harita kontrolü yapar. Tuzak ve cihazlarla site bekler. Takımın güvenlik duvarı.</p>
        <div class="agents-list">
          <span class="agent-pill">Killjoy</span>
          <span class="agent-pill">Cypher</span>
          <span class="agent-pill">Sage</span>
          <span class="agent-pill">Vyse</span>
          <span class="agent-pill">Chamber</span>
        </div>
      </div>
      <div class="role-card reveal">
        <div class="role-icon">🔍</div>
        <h3>Initiator – Başlatıcı</h3>
        <p>Düşman bilgisi toplar. Flash ve stun atar. Duelist'e yol açar ve siteye giriş kolaylaştırır.</p>
        <div class="agents-list">
          <span class="agent-pill">Sova</span>
          <span class="agent-pill">Fade</span>
          <span class="agent-pill">Skye</span>
          <span class="agent-pill">Gekko</span>
          <span class="agent-pill">Breach</span>
        </div>
      </div>
      <div class="role-card reveal">
        <div class="role-icon">💨</div>
        <h3>Controller – Kontrolcü</h3>
        <p>Duman atar, alan kontrolü yapar. Düşmanların görmesini engeller. Takımın stratejistik beini.</p>
        <div class="agents-list">
          <span class="agent-pill">Omen</span>
          <span class="agent-pill">Viper</span>
          <span class="agent-pill">Brimstone</span>
          <span class="agent-pill">Astra</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- MAPS -->
<section id="maps" style="background:#0d0e10;">
  <div class="section-inner">
    <div class="section-header reveal">
      <div class="tag">Harita Rehberi</div>
      <h2>TÜM <span>HARITALAR</span></h2>
      <p>12 haritanın hepsini, önerilenen ajanları ve stratejileri incele.</p>
    </div>
    <div class="filter-bar reveal">
      <button class="filter-btn active" onclick="filterMaps('all')">Tümü</button>
      <button class="filter-btn" onclick="filterMaps('comp')">Kompetitif</button>
      <button class="filter-btn" onclick="filterMaps('casual')">Casual</button>
      <button class="filter-btn" onclick="filterMaps('3site')">3 Site</button>
    </div>
    <div class="maps-grid" id="mapsGrid">
      <!-- Maps injected by JS -->
    </div>
  </div>
</section>

<!-- TEAM COMPS -->
<section id="comps">
  <div class="section-inner">
    <div class="section-header reveal">
      <div class="tag">Takım Kurma</div>
      <h2>EN İYİ <span>TAKIM KOMPOZYONLARI</span></h2>
      <p>Her harita için profesyonelların kullandığı en iyi 5'li kompozyonlar.</p>
    </div>
    <div class="comp-cards" id="compCards">
      <!-- Comps injected by JS -->
    </div>
  </div>
</section>

<!-- TIPS -->
<section id="tips" style="background:#0d0e10;">
  <div class="section-inner">
    <div class="section-header reveal">
      <div class="tag">Yeni Başlangıç</div>
      <h2>BAŞLANGIÇ <span>İPUÇLARI</span></h2>
      <p>Rankedde yükselmek için bilmen gerekenleri öğren.</p>
    </div>
    <div class="tips-grid" id="tipsGrid">
      <!-- Tips injected by JS -->
    </div>
  </div>
</section>

<!-- TIER LIST -->
<section id="tiers">
  <div class="section-inner">
    <div class="section-header reveal">
      <div class=
