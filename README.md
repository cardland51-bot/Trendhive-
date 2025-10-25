<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>TrendHive — Mobile Pitch Deck</title>
<style>
  /* === Brand colors === */
  :root{
    --primary: #F6C85F; /* honey */
    --accent:  #FF6F61; /* coral */
    --dark:    #0B2545; /* navy */
    --muted:   #f4f6f8;
    --card:    #ffffff;
    --glass:   rgba(255,255,255,0.85);
    --radius: 14px;
    --maxw:   980px;
  }

  /* === Global reset & base === */
  *{box-sizing:border-box}
  html,body{height:100%;margin:0;font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial; background:linear-gradient(180deg,#fbfdff 0%, #eef4f8 100%); color:var(--dark); -webkit-font-smoothing:antialiased;}
  a{color:var(--accent);text-decoration:none}
  .container{max-width:var(--maxw);margin:14px auto;padding:12px; }

  /* === Slide deck === */
  .deck{
    height: calc(100vh - 32px);
    display:flex;
    align-items:center;
    justify-content:center;
    position:relative;
  }
  .slide {
    width:100%;
    max-width:900px;
    height:100%;
    background:var(--card);
    border-radius:var(--radius);
    box-shadow: 0 18px 40px rgba(11,37,69,0.10);
    padding:18px;
    display:flex;
    flex-direction:column;
    gap:12px;
    overflow:hidden;
    position:absolute;
    left:0; top:0;
    transition: transform 330ms cubic-bezier(.2,.9,.3,1), opacity 250ms;
  }
  .slide.hidden { opacity:0; pointer-events:none; transform:translateY(8px) scale(.997); }
  .slide.visible { opacity:1; pointer-events:auto; transform:none; }

  /* === Header / logo === */
  .header{
    display:flex;align-items:center;gap:12px;
  }
  .logo {
    width:56px;height:56px;border-radius:12px;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,var(--primary),#FFD77A);
    box-shadow: inset 0 -6px 14px rgba(255,255,255,0.22);
  }
  .brand h1{margin:0;font-size:18px;color:var(--dark)}
  .brand p{margin:0;font-size:12px;color:#39526f;opacity:.95}

  /* === Content blocks === */
  h2{margin:8px 0 6px;color:var(--dark);font-size:18px}
  p.lead{margin:0;color:#425a78;font-size:14px;line-height:1.35}
  .row {display:flex;gap:12px;align-items:flex-start;flex-wrap:wrap}
  .card{background:var(--muted);padding:12px;border-radius:10px;border:1px solid rgba(11,37,69,0.035);}

  /* === small stat pills === */
  .pills{display:flex;gap:8px;flex-wrap:wrap}
  .pill{background:var(--card);padding:8px 10px;border-radius:999px;box-shadow:0 6px 14px rgba(11,37,69,0.04);font-weight:700;font-size:13px}
  .pill.accent{background:linear-gradient(90deg,var(--accent),#FF8D7E);color:white}

  /* === Feed mock === */
  .feed{background:linear-gradient(180deg,#fff,#fbfdff);padding:8px;border-radius:10px;height:100%;overflow:auto;border:1px solid rgba(11,37,69,0.03)}
  .feed-item{padding:10px;border-radius:8px;margin-bottom:8px;background:#fff;box-shadow:0 6px 14px rgba(11,37,69,0.03)}
  .feed-item h4{margin:0;font-size:13px;color:var(--dark)}
  .feed-item p{margin:6px 0 0;font-size:12px;color:#66798f}

  /* === Workflow SVG container === */
  .workflow{display:flex;justify-content:center;padding:6px 0}
  .wf-box{display:flex;align-items:center;gap:10px;flex-wrap:wrap;justify-content:center}
  .wf-node{background:linear-gradient(180deg,#fff,#fff9ea);border:1px solid rgba(11,37,69,0.04);padding:10px 12px;border-radius:10px;box-shadow:0 8px 20px rgba(11,37,69,0.04);font-weight:700;font-size:13px;color:var(--dark);min-width:80px;text-align:center}
  .wf-arrow{font-weight:800;color:#8aa0bf}

  /* === Timeline (rollout plan) === */
  .timeline{display:flex;flex-direction:column;gap:12px;padding:8px}
  .t-step{display:flex;gap:12px;align-items:flex-start}
  .t-dot{width:12px;height:12px;border-radius:999px;background:var(--primary);box-shadow:0 6px 14px rgba(246,200,95,0.18);margin-top:4px}
  .t-card{background:#fff;padding:10px;border-radius:10px;border:1px solid rgba(11,37,69,0.03);flex:1}
  .t-card h4{margin:0 0 6px;font-size:14px}
  .t-card p{margin:0;font-size:13px;color:#556a86}

  /* === Controls (big for mobile) === */
  .controls{position:fixed;left:50%;transform:translateX(-50%);bottom:18px;display:flex;gap:10px;align-items:center;z-index:1200}
  .btn{background:var(--card);border-radius:999px;padding:12px 16px;border:0;box-shadow:0 12px 30px rgba(11,37,69,0.09);font-weight:800;cursor:pointer}
  .btn.primary{background:linear-gradient(90deg,var(--primary),#FFD77A);color:var(--dark)}
  .page-ind{background:rgba(255,255,255,0.88);padding:10px 12px;border-radius:999px}

  /* === Footer small === */
  .footer{font-size:12px;color:#6d839d;text-align:center;padding:8px}

  /* === Responsive tweaks === */
  @media (max-width:600px){
    .slide{padding:14px;border-radius:12px}
    h2{font-size:16px}
    .brand h1{font-size:16px}
    .feed{height:160px}
    .wf-node{min-width:72px;padding:8px;font-size:12px}
  }

  /* === Print / one-pager toggles === */
  .printable {display:none}
  @media print {
    body{background:white}
    .controls, .feed, .btn, .page-ind, .logo {display:none}
    .slide{position:static;box-shadow:none;border-radius:0;padding:10px}
    .printable{display:block}
  }

</style>
</head>
<body>

<div class="container">
  <div class="deck" id="deck" role="region" aria-label="TrendHive pitch deck">
    <!-- Slide: Cover -->
    <section class="slide visible" data-index="0" id="slide-0" tabindex="0">
      <div class="header">
        <div class="logo" aria-hidden="true">
          <!-- Inline logo SVG -->
          <svg viewBox="0 0 64 64" width="44" height="44" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <defs><linearGradient id="g2" x1="0" x2="1"><stop offset="0" stop-color="#F6C85F"/><stop offset="1" stop-color="#FFD77A"/></linearGradient></defs>
            <rect x="6" y="6" width="52" height="52" rx="10" fill="url(#g2)"/>
            <path d="M20 40c5 4 12 4 17 0" stroke="#0B2545" stroke-width="2.5" stroke-linecap="round"/>
            <path d="M24 30c3-5 9-5 12 0" stroke="#0B2545" stroke-width="2.5" stroke-linecap="round"/>
            <circle cx="32" cy="20" r="2.6" fill="#0B2545"/>
          </svg>
        </div>
        <div class="brand">
          <h1>TrendHive</h1>
          <p>Buzz faster. Know earlier.</p>
        </div>
        <div style="margin-left:auto">
          <div class="pill accent" style="font-size:12px;padding:8px 14px">Mobile-first • Real-time • Adaptive</div>
        </div>
      </div>

      <div style="margin-top:10px">
        <h2>What is TrendHive?</h2>
        <p class="lead">A mobile-first system that detects emerging trends and sends short, actionable alerts to users before those trends go mainstream. Designed to be fast, private, and adaptive to each user's behaviour.</p>
      </div>

      <div style="display:flex;gap:12px;margin-top:12px;flex-wrap:wrap">
        <div class="card" style="flex:1">
          <h2 style="font-size:15px;margin-bottom:8px">Problem</h2>
          <ul style="margin:0 0 0 16px;color:#2f4e6d">
            <li>Teams miss first-mover opportunities</li>
            <li>Existing tools are noisy & slow</li>
            <li>Personalization is clumsy or absent</li>
          </ul>
        </div>

        <div class="card" style="min-width:160px">
          <h2 style="font-size:15px;margin-bottom:8px">Solution</h2>
          <ul style="margin:0 0 0 16px;color:#2f4e6d">
            <li>Real-time ingestion & scoring</li>
            <li>Instant push notifications</li>
            <li>Behavioral learning & prioritization</li>
          </ul>
        </div>
      </div>

      <div style="margin-top:auto;display:flex;justify-content:space-between;align-items:center">
        <div style="font-size:13px;color:#58708c">Slide 1 / 5</div>
        <div style="font-size:12px;color:#7a90a9">Mobile-optimized pitch</div>
      </div>
    </section>

    <!-- Slide: Market & Audience -->
    <section class="slide hidden" data-index="1" id="slide-1" tabindex="0">
      <div class="header">
        <div class="logo" style="width:48px;height:48px"></div>
        <div class="brand"><h1 style="font-size:16px">Market & Audience</h1><p style="font-size:12px;color:#5b6f85">Where TrendHive fits</p></div>
      </div>

      <div style="margin-top:8px">
        <h2>Who benefits?</h2>
        <div class="row" style="gap:8px">
          <div class="card" style="flex:1">
            <ul style="margin:0 0 0 16px;color:#2f4e6d">
              <li>Social teams & creators</li>
              <li>Brands & product managers</li>
              <li>PR / rapid response teams</li>
              <li>Market analysts</li>
            </ul>
          </div>

          <div style="width:200px">
            <div class="feed">
              <div class="feed-item"><h4>Snack Trend</h4><p>Micro-influencer mentions rising 410%</p></div>
              <div class="feed-item"><h4>Audio Hook</h4><p>New sound format popping on short video</p></div>
              <div class="feed-item"><h4>Retail Buzz</h4><p>Local search spiking in one city</p></div>
            </div>
          </div>
        </div>
      </div>

      <div style="margin-top:auto;display:flex;justify-content:space-between">
        <div style="font-size:13px;color:#58708c">Slide 2 / 5</div>
        <div class="pill">Go-to-market: freemium → pro → enterprise</div>
      </div>
    </section>

    <!-- Slide: Framework & Workflow -->
    <section class="slide hidden" data-index="2" id="slide-2" tabindex="0">
      <div class="header">
        <div class="logo"></div>
        <div class="brand"><h1 style="font-size:16px">Framework & Workflow</h1><p style="font-size:12px;color:#5b6f85">How data becomes an alert</p></div>
      </div>

      <div style="margin-top:8px">
        <h2>System workflow (conceptual)</h2>
        <div class="workflow" aria-hidden="false">
          <div class="wf-box" role="img" aria-label="Data pipeline">
            <div class="wf-node">Data<br><small style="font-weight:400">(APIs, RSS, Social)</small></div>
            <div class="wf-arrow">→</div>
            <div class="wf-node">Ingest<br><small style="font-weight:400">(Collectors & Queue)</small></div>
            <div class="wf-arrow">→</div>
            <div class="wf-node">Analyze<br><small style="font-weight:400">(NLP / Scoring)</small></div>
            <div class="wf-arrow">→</div>
            <div class="wf-node">Score<br><small style="font-weight:400">(Trend & Urgency)</small></div>
            <div class="wf-arrow">→</div>
            <div class="wf-node">Notify<br><small style="font-weight:400">(OneSignal, FCM, PWA)</small></div>
            <div class="wf-arrow">→</div>
            <div class="wf-node">Learn<br><small style="font-weight:400">(Feedback loop)</small></div>
          </div>
        </div>

        <div style="margin-top:12px">
          <h2 style="font-size:15px">Technical notes</h2>
          <div class="row" style="gap:10px">
            <div class="card" style="flex:1">
              <strong>Collectors</strong>
              <p style="margin:6px 0 0;font-size:13px;color:#556a86">Connectors to APIs, webhooks, RSS and streaming endpoints (serverless or small EC2).</p>
            </div>
            <div class="card" style="flex:1">
              <strong>Analyze</strong>
              <p style="margin:6px 0 0;font-size:13px;color:#556a86">Lightweight NLP, signal detection, spike detection, and lightweight ML scoring. Cloud for heavy models.</p>
            </div>
          </div>
        </div>
      </div>

      <div style="margin-top:auto;display:flex;justify-content:space-between">
        <div style="font-size:13px;color:#58708c">Slide 3 / 5</div>
        <div style="font-size:12px;color:#7a90a9">Latency target: <strong>&lt; 2 minutes</strong></div>
      </div>
    </section>

    <!-- Slide: Rollout Plan (timeline) -->
    <section class="slide hidden" data-index="3" id="slide-3" tabindex="0">
      <div class="header">
        <div class="logo"></div>
        <div class="brand"><h1 style="font-size:16px">Rollout Plan</h1><p style="font-size:12px;color:#5b6f85">Stepwise launch — fast & measurable</p></div>
      </div>

      <div style="margin-top:8px">
        <h2>90-day rollout (high level)</h2>
        <div class="timeline">
          <div class="t-step">
            <div class="t-dot" aria-hidden="true"></div>
            <div class="t-card">
              <h4>Phase 1 — Week 1</h4>
              <p>Wireframes, basic push integration, and one simple trigger (e.g., Twitter/RSS spike → test alert).</p>
            </div>
          </div>

          <div class="t-step">
            <div class="t-dot"></div>
            <div class="t-card">
              <h4>Phase 2 — Week 2–4</h4>
              <p>No-code PWA or Glide app, OneSignal setup, 10–50 beta users, tune alert precision.</p>
            </div>
          </div>

          <div class="t-step">
            <div class="t-dot"></div>
            <div class="t-card">
              <h4>Phase 3 — Month 2</h4>
              <p>Creator onboarding, support flows, add analytics & alert history, iterate UX.</p>
            </div>
          </div>

          <div class="t-step">
            <div class="t-dot"></div>
            <div class="t-card">
              <h4>Phase 4 — Month 3</h4>
              <p>Public launch, tiered subscription rollout, partner integrations (Slack, Teams), measure DAU.</p>
            </div>
          </div>
        </div>
      </div>

      <div style="margin-top:auto;display:flex;justify-content:space-between">
        <div style="font-size:13px;color:#58708c">Slide 4 / 5</div>
        <div style="font-size:12px;color:#7a90a9">Measure: alert latency, DAU, conversion</div>
      </div>
    </section>

    <!-- Slide: Business Model & Contact (no funding ask) -->
    <section class="slide hidden" data-index="4" id="slide-4" tabindex="0">
      <div class="header">
        <div class="logo"></div>
        <div class="brand"><h1 style="font-size:16px">Business Model & Contact</h1><p style="font-size:12px;color:#5b6f85">How TrendHive operates</p></div>
      </div>

      <div style="margin-top:8px">
        <h2>Business model</h2>
        <div class="row" style="gap:12px;align-items:flex-start">
          <div class="card" style="flex:1">
            <ul style="margin:0 0 0 16px;color:#2f4e6d">
              <li>Freemium core (basic alerts)</li>
              <li>Pro subscription: advanced filters, priority alerts, analytics</li>
              <li>Enterprise: integrations, API access, SLAs</li>
              <li>Sponsored alert & partnership opportunities</li>
            </ul>
          </div>

          <div style="width:200px">
            <div class="card" style="text-align:center">
              <h3 style="margin:0 0 8px;color:var(--accent)">Metrics targets</h3>
              <p style="margin:0;font-size:13px;color:#4f6b8a">500 DAU • 10% pro conversion • alert latency &lt; 2 min</p>
            </div>
          </div>
        </div>

        <div style="margin-top:12px">
          <h2>Contact</h2>
          <p class="lead" style="margin:0">Email: <strong>hello@trendhive.example</strong><br>Demo link / signups: <strong>trendhive.app/demo</strong></p>
        </div>

        <div style="margin-top:12px">
          <button class="btn" id="onepagerBtn" title="Download one-page printable">Download one-pager (print)</button>
        </div>
      </div>

      <div style="margin-top:auto" class="footer">© <strong>TrendHive</strong> — Be first, not loud.</div>
    </section>

  </div>

  <!-- controls -->
  <div class="controls" role="group" aria-label="Deck controls">
    <button class="btn" id="prevBtn" aria-label="Previous">◀ Prev</button>
    <div class="page-ind" id="pageInd">1 / 5</div>
    <button class="btn primary" id="nextBtn" aria-label="Next">Next ▶</button>
  </div>
</div>

<script>
/* === Slide navigation and mobile gestures === */
(function(){
  const slides = Array.from(document.querySelectorAll('.slide'));
  const total = slides.length;
  let index = 0;
  const pageInd = document.getElementById('pageInd');

  function show(i){
    index = Math.max(0, Math.min(total-1, i));
    slides.forEach((s,si)=>{
      s.classList.remove('visible','hidden');
      if(si === index) s.classList.add('visible');
      else s.classList.add('hidden');
    });
    pageInd.textContent = (index+1) + ' / ' + total;
    window.scrollTo({top:0,behavior:'smooth'});
    // focus for screen readers
    slides[index].focus && slides[index].focus();
  }

  document.getElementById('prevBtn').addEventListener('click',()=> show(index-1));
  document.getElementById('nextBtn').addEventListener('click',()=> show(index+1));

  // keyboard
  window.addEventListener('keydown', (e)=>{
    if(e.key === 'ArrowLeft') show(index-1);
    if(e.key === 'ArrowRight') show(index+1);
  });

  // touch swipe
  let startX = 0;
  document.addEventListener('touchstart', (e)=> startX = e.changedTouches[0].screenX);
  document.addEventListener('touchend', (e)=>{
    const dx = e.changedTouches[0].screenX - startX;
    if(dx < -40) show(index+1);
    if(dx > 40) show(index-1);
  });

  // deep-link via #slide=#
  const h = location.hash.match(/slide=(\d+)/);
  if(h) show(Math.max(0, Math.min(total-1, Number(h[1]) - 1)));
  else show(0);

  // one-pager print button -> open printable view
  document.getElementById('onepagerBtn').addEventListener('click', ()=> {
    // open a printable window containing condensed content
    const content = `
      <html><head><meta name="viewport" content="width=device-width,initial-scale=1"><title>TrendHive One-Pager</title>
      <style>body{font-family:system-ui,-apple-system,Segoe UI,Roboto;line-height:1.4;color:#122; padding:18px} h1{color:${'#0B2545'}} .hl{color:${'#FF6F61'}} .box{border:1px solid #dde6f0;padding:10px;border-radius:8px;margin:12px 0}</style>
      </head><body>
      <h1>TrendHive — One Pager</h1>
      <div class="box"><h3>What</h3><p>Real-time trend detection & push alerts — mobile-first.</p></div>
      <div class="box"><h3>How</h3><p>Data → Ingest → Analyze → Score → Notify → Learn (adaptive feedback loop).</p></div>
      <div class="box"><h3>Rollout</h3><p>Week1: test alerts. Week2-4: beta & tune. Month2: creators. Month3: public launch.</p></div>
      <div class="box"><h3>Business Model</h3><p>Freemium, Pro subs, Enterprise API, Sponsored alerts.</p></div>
      <div style="margin-top:12px">Contact: hello@trendhive.example</div>
      </body></html>`;
    const win = window.open('', '_blank');
    win.document.write(content);
    win.document.close();
  });

})();
</script>

</body>
</html>
