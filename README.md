<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>TrendHive — Pitch Deck</title>

<!-- Google Font -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">

<style>
  :root{
    --primary: #F6C85F;   /* honey */
    --accent:  #FF6F61;   /* coral */
    --dark:    #0B2545;   /* navy */
    --muted:   #F4F6F8;
    --card:    #ffffff;
    --glass:   rgba(255,255,255,0.7);
    --radius: 16px;
  }

  html,body{height:100%;margin:0;background:linear-gradient(180deg,#f8fafb 0%, #eef4f8 100%);font-family:'Inter',system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial;}
  .deck {
    max-width:1100px;
    margin:28px auto;
    height: calc(100vh - 56px);
    display:grid;
    grid-template-columns: 1fr;
    align-items:center;
    justify-items:center;
    position:relative;
    padding:18px;
  }

  .slide {
    width:100%;
    height:100%;
    background:var(--card);
    border-radius:var(--radius);
    box-shadow: 0 18px 40px rgba(11,37,69,0.12);
    padding:36px;
    box-sizing:border-box;
    display:flex;
    flex-direction:column;
    gap:18px;
    transform: translateX(0);
    transition: transform 350ms cubic-bezier(.2,.9,.3,1), opacity 300ms;
    opacity:1;
  }

  .slide.hidden { opacity:0; pointer-events:none; transform: translateX(30px) scale(.995); }

  header.top {
    display:flex;
    align-items:center;
    gap:16px;
  }

  .logo-wrap{
    display:flex;align-items:center;gap:12px;
  }
  .logo {
    width:64px;height:64px;border-radius:12px;background:linear-gradient(135deg,var(--primary),#FFD77A);
    display:flex;align-items:center;justify-content:center;box-shadow: inset 0 -6px 14px rgba(255,255,255,0.25);
  }

  /* simple SVG bee mark inside */
  .logo svg{width:40px;height:40px;display:block}

  .brand {
    line-height:1;
  }
  .brand h1{margin:0;font-size:20px;color:var(--dark);letter-spacing:0.2px;}
  .brand p{margin:0;font-size:12px;color:#385072;opacity:0.95}

  .hero {
    display:flex;
    gap:28px;
    align-items:center;
    justify-content:space-between;
    flex-wrap:wrap;
  }

  .hero .left {
    flex:1 1 420px;
  }
  .tag {
    display:inline-block;
    background:linear-gradient(90deg,var(--accent),#FF8D7E);
    color:white;padding:6px 12px;border-radius:999px;font-weight:700;font-size:12px;
  }

  h2 {color:var(--dark);margin:8px 0 6px;font-size:22px;}
  p.lead {color:#405a77;margin:0 0 6px;font-size:15px;}

  .stats {
    display:flex;gap:12px;margin-top:10px;
  }
  .stat {
    background:linear-gradient(180deg,#fff,#fbfbfb);
    padding:12px 14px;border-radius:12px;box-shadow:0 6px 18px rgba(11,37,69,0.05);
    min-width:120px;text-align:center;
  }
  .stat strong{display:block;font-size:20px;color:var(--dark)}
  .stat span{font-size:12px;color:#6b8096}

  .content-grid {display:grid;grid-template-columns:1fr 340px;gap:20px;margin-top:8px;align-items:start;}
  .card {
    background:var(--muted);padding:16px;border-radius:12px;border:1px solid rgba(11,37,69,0.03);
  }
  ul {margin:0;padding-left:18px;color:#334a64}
  li {margin:8px 0}

  /* sidebar feed mock */
  .feed {background:linear-gradient(180deg,#ffffff,#fbfdff);padding:12px;border-radius:12px;height:100%;overflow:auto;border:1px solid rgba(11,37,69,0.03)}
  .feed-item{padding:10px;border-radius:10px;margin-bottom:8px;background:#fff;box-shadow:0 6px 14px rgba(11,37,69,0.03)}
  .feed-item h4{margin:0;font-size:13px;color:var(--dark)}
  .feed-item p{margin:4px 0 0;font-size:12px;color:#65788f}

  /* controls */
  .controls {
    position:absolute;left:18px;right:18px;bottom:-12px;display:flex;justify-content:space-between;align-items:center;pointer-events:none;
  }
  .nav {
    pointer-events:auto;background:var(--card);border-radius:999px;padding:8px;display:flex;gap:8px;box-shadow:0 6px 18px rgba(11,37,69,0.08);
  }
  .nav button{background:transparent;border:0;padding:8px 12px;border-radius:10px;font-weight:700;cursor:pointer;color:var(--dark)}
  .nav button.primary{background:linear-gradient(90deg,var(--primary),#FFD77A);color:var(--dark);box-shadow:0 8px 20px rgba(246,200,95,0.18)}
  .page-indicator{pointer-events:auto;background:rgba(255,255,255,0.7);padding:8px 12px;border-radius:999px;font-size:13px;color:#5e748f}

  /* footer small */
  .micro {font-size:12px;color:#7b8ea6;margin-top:8px}

  /* responsive */
  @media (max-width:900px){
    .content-grid{grid-template-columns:1fr; }
    .feed{order:2}
    .hero{flex-direction:column;align-items:flex-start}
    .logo{width:56px;height:56px}
  }

  /* transition slide left/right */
  .slide.left { transform: translateX(-36px) scale(.997); opacity:0; pointer-events:none; }
  .slide.right { transform: translateX(36px) scale(.997); opacity:0; pointer-events:none; }

  /* small fancy highlight */
  .pill {display:inline-block;padding:6px 10px;border-radius:999px;background:rgba(255,111,97,0.12);color:var(--accent);font-weight:700;font-size:12px}
</style>
</head>
<body>

<div class="deck" id="deck">
  <!-- Slide 0: Cover -->
  <section class="slide" data-index="0" id="s0">
    <header class="top">
      <div class="logo-wrap">
        <div class="logo" aria-hidden="true">
          <!-- Inline SVG: stylized bee / hive mark -->
          <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="TrendHive logo">
            <defs><linearGradient id="g" x1="0" x2="1"><stop offset="0" stop-color="#F6C85F"/><stop offset="1" stop-color="#FFD77A"/></linearGradient></defs>
            <rect x="6" y="6" width="52" height="52" rx="10" fill="url(#g)"/>
            <path d="M20 40c5 4 12 4 17 0" stroke="#0B2545" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M24 30c3-5 9-5 12 0" stroke="#0B2545" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
            <circle cx="32" cy="20" r="2.6" fill="#0B2545"/>
          </svg>
        </div>
        <div class="brand">
          <h1>TrendHive</h1>
          <p>Buzz faster. Know earlier.</p>
        </div>
      </div>

      <div style="margin-left:auto;text-align:right">
        <div class="pill">MVP • Real-time Alerts • Adaptive AI</div>
      </div>
    </header>

    <div class="hero" style="margin-top:8px;">
      <div class="left">
        <h2>Catch the wave before it becomes a tide</h2>
        <p class="lead">TrendHive monitors social signals and news in real-time and sends short, actionable alerts directly to users' phones so they can act first.</p>

        <div class="stats" style="margin-top:14px;">
          <div class="stat"><strong>Real-time</strong><span>Seconds → minutes</span></div>
          <div class="stat"><strong>Personal</strong><span>Learns your interests</span></div>
          <div class="stat"><strong>Mobile-first</strong><span>Push & PWA</span></div>
        </div>
      </div>

      <div style="width:360px">
        <div class="card">
          <h3 style="margin:0 0 8px;color:var(--accent)">Concept Snapshot</h3>
          <ul>
            <li>Fast alerts — push notifications & short summaries</li>
            <li>Adaptive filters that learn from behavior</li>
            <li>No-code MVP → scale to AI back-end</li>
          </ul>
          <div class="micro">Perfect for marketers, creators, and analysts.</div>
        </div>
      </div>
    </div>

    <div style="margin-top:18px;display:flex;gap:12px;flex-wrap:wrap">
      <div class="card" style="flex:1 1 300px">
        <h3 style="margin:0 0 8px">Problem</h3>
        <ul>
          <li>Missed first-mover opportunities</li>
          <li>Noise vs signal — hard to find what's real</li>
          <li>Teams react too slowly</li>
        </ul>
      </div>

      <div class="card" style="flex:1 1 300px">
        <h3 style="margin:0 0 8px">Solution</h3>
        <ul>
          <li>Real-time trend detection</li>
          <li>Instant push + tap-to-expand details</li>
          <li>Adaptive personalization</li>
        </ul>
      </div>
    </div>

    <div class="micro" style="margin-top:auto">Slide 1 of 6</div>
  </section>

  <!-- Slide 1: Market & Audience -->
  <section class="slide hidden" data-index="1" id="s1">
    <header class="top">
      <div class="logo-wrap" style="gap:12px">
        <div class="logo" style="width:56px;height:56px"><svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg"><rect x="6" y="6" width="52" height="52" rx="10" fill="url(#g)"/></svg></div>
        <div>
          <h1 style="font-size:16px">TrendHive — Market</h1>
          <p style="font-size:12px;color:#5b6f85;margin-top:4px">Opportunity | early mover advantage</p>
        </div>
      </div>
    </header>

    <div style="display:flex;gap:20px;margin-top:18px;align-items:flex-start;flex-wrap:wrap">
      <div style="flex:1 1 520px">
        <h2>Who benefits?</h2>
        <ul>
          <li>Social & content teams who need first-mover content</li>
          <li>Brands launching time-sensitive campaigns</li>
          <li>Influencers and creators hunting viral topics</li>
          <li>Market analysts & rapid-response PR teams</li>
        </ul>

        <h2 style="margin-top:18px">Go-to-market</h2>
        <ul>
          <li>Freemium consumer app + paid pro tier</li>
          <li>Enterprise integrations (Slack, Teams, API)</li>
          <li>Sponsored trend alerts & brand partnerships</li>
        </ul>
      </div>

      <div style="width:320px">
        <div class="feed">
          <div class="feed-item"><h4>Viral Sprout: melon drink trend</h4><p>Spiked 420% in micro-influencer posts</p></div>
          <div class="feed-item"><h4>Finance: microcap mention uptick</h4><p>Community-driven momentum detected</p></div>
          <div class="feed-item"><h4>Fashion: neon resurface</h4><p>Signals across TikTok & Pins</p></div>
          <div class="feed-item"><h4>Music: hook sound emergence</h4><p>New audio format climbing</p></div>
        </div>
      </div>
    </div>

    <div class="micro" style="margin-top:auto">Slide 2 of 6</div>
  </section>

  <!-- Slide 2: Product -->
  <section class="slide hidden" data-index="2" id="s2">
    <header class="top">
      <div class="logo-wrap"><div class="logo" style="width:56px;height:56px"><svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg"></svg></div>
      <div><h1 style="font-size:16px">Product</h1><p style="font-size:12px;color:#5b6f85;margin-top:4px">MVP → Intelligent system</p></div></div>
    </header>

    <div class="content-grid" style="margin-top:12px">
      <div>
        <h2>Core features (MVP)</h2>
        <ul>
          <li>Fast alerts via OneSignal / FCM (PWA + native)</li>
          <li>Simple onboarding & preference toggles</li>
          <li>Data triggers: RSS, social signals, keyword spikes</li>
          <li>Basic behavior tracking (open / ignore) for learning</li>
        </ul>

        <h2 style="margin-top:12px">Full-term vision</h2>
        <ul>
          <li>Predictive filtering & trend scoring</li>
          <li>Enterprise API + integrations</li>
          <li>Automated content suggestions for creators</li>
        </ul>
      </div>

      <aside class="feed">
        <div style="font-weight:700;margin-bottom:8px">MVP Tech Stack</div>
        <div class="feed-item"><h4>Frontend</h4><p>Glide / PWA / Adalo (mobile-first)</p></div>
        <div class="feed-item"><h4>Notifications</h4><p>OneSignal + Firebase Cloud Messaging</p></div>
        <div class="feed-item"><h4>Backend</h4><p>Firebase Functions or small Node + Postgres</p></div>
        <div class="feed-item"><h4>Automation</h4><p>Zapier / Make for quick triggers</p></div>
      </aside>
    </div>

    <div class="micro" style="margin-top:auto">Slide 3 of 6</div>
  </section>

  <!-- Slide 3: Business Model -->
  <section class="slide hidden" data-index="3" id="s3">
    <header class="top">
      <div class="logo-wrap"><div class="logo" style="width:56px;height:56px"></div><div><h1 style="font-size:16px">Business Model</h1><p style="font-size:12px;color:#5b6f85;margin-top:4px">How TrendHive makes money</p></div></div>
    </header>

    <div style="display:flex;gap:16px;margin-top:12px;flex-wrap:wrap">
      <div style="flex:1 1 560px">
        <h2>Revenue streams</h2>
        <ul>
          <li>Freemium → subscriptions for pro features</li>
          <li>Enterprise licensing & API access</li>
          <li>Sponsored trend campaigns & alerts</li>
          <li>Data licensing to research/marketing teams</li>
        </ul>

        <h2 style="margin-top:12px">Early growth tactics</h2>
        <ul>
          <li>Beta invites to creators and agencies</li>
          <li>Case studies showing first-mover wins</li>
          <li>Partnerships with social analytics platforms</li>
        </ul>
      </div>

      <div style="width:320px">
        <div class="card">
          <h3 style="margin:0 0 8px">Unit economics (example)</h3>
          <p style="margin:0">Assume: $10/mo pro user; CAC $20; LTV 24 months → strong margins at scale.</p>
        </div>
      </div>
    </div>

    <div class="micro" style="margin-top:auto">Slide 4 of 6</div>
  </section>

  <!-- Slide 4: Roadmap & Ask -->
  <section class="slide hidden" data-index="4" id="s4">
    <header class="top">
      <div class="logo-wrap"><div class="logo" style="width:56px;height:56px"></div><div><h1 style="font-size:16px">Roadmap & Ask</h1><p style="font-size:12px;color:#5b6f85;margin-top:4px">How to ship fast</p></div></div>
    </header>

    <div style="display:flex;gap:16px;margin-top:12px;flex-wrap:wrap">
      <div style="flex:1 1 560px">
        <h2>90-day roadmap (MVP)</h2>
        <ul>
          <li>Week 1: Wireframes, push integration, test alerts</li>
          <li>Week 2: No-code app (Glide/Adalo) + OneSignal setup</li>
          <li>Week 3–6: Beta testing, tune triggers, onboard creators</li>
          <li>Month 3: Subscription flow & basic analytics</li>
        </ul>

        <h2 style="margin-top:12px">Ask</h2>
        <ul>
          <li>Funding: $25k to ship MVP + initial user acquisition</li>
          <li>Intro: 50 beta users (influencers / agencies)</li>
          <li>Technical: cloud credits for scaling pipelines</li>
        </ul>
      </div>

      <div style="width:320px">
        <div class="card">
          <h3 style="margin:0 0 8px">Metrics to hit</h3>
          <ul style="margin:0">
            <li>500 DAU within 60 days</li>
            <li>10% conversion to pro in first 90 days</li>
            <li>Average alert latency < 2 minutes</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="micro" style="margin-top:auto">Slide 5 of 6</div>
  </section>

  <!-- Slide 5: Team & Contact -->
  <section class="slide hidden" data-index="5" id="s5">
    <header class="top">
      <div class="logo-wrap"><div class="logo" style="width:56px;height:56px"></div><div><h1 style="font-size:16px">Team & Contact</h1><p style="font-size:12px;color:#5b6f85;margin-top:4px">Who makes it happen</p></div></div>
    </header>

    <div style="display:flex;gap:18px;margin-top:12px;flex-wrap:wrap;align-items:stretch">
      <div style="flex:1 1 520px">
        <h2>Team</h2>
        <ul>
          <li>Product & Strategy — Paul (you) — vision & ops</li>
          <li>Engineering — Backend & alerts — initial freelance / cloud</li>
          <li>Growth — creators & partnerships — early hires</li>
        </ul>

        <h2 style="margin-top:12px">Contact</h2>
        <p class="lead" style="margin:0">Email: <strong>hello@trendhive.example</strong> • Demo + signups: <strong>trendhive.app/demo</strong></p>
      </div>

      <div style="width:320px">
        <div class="card" style="text-align:center">
          <h3 style="margin:0 0 8px;color:var(--accent)">Closing</h3>
          <p style="margin:0">“Be first, not loud.”</p>
          <div style="margin-top:10px;font-size:12px;color:#6b8096">Thank you — let’s build it.</div>
        </div>
      </div>
    </div>

    <div class="micro" style="margin-top:auto">Slide 6 of 6</div>
  </section>

  <!-- controls -->
  <div class="controls" aria-hidden="false">
    <div class="nav" role="navigation" aria-label="Slide navigation">
      <button id="prevBtn" title="Previous">◀</button>
      <div class="page-indicator" id="page">1 / 6</div>
      <button id="nextBtn" class="primary" title="Next">Next ▶</button>
    </div>
  </div>
</div>

<script>
  (function(){
    const slides = Array.from(document.querySelectorAll('.slide'));
    let idx = 0;
    const page = document.getElementById('page');
    const total = slides.length;

    function show(i){
      slides.forEach((s,si)=>{
        s.classList.remove('left','right','hidden');
        if(si < i) s.classList.add('left');
        if(si > i) s.classList.add('right');
        if(si !== i) s.classList.add('hidden');
      });
      idx = Math.max(0, Math.min(i, total-1));
      page.textContent = (idx+1) + ' / ' + total;
      // small accessibility focus
      slides[idx].focus && slides[idx].focus();
    }

    document.getElementById('prevBtn').addEventListener('click',()=> show(idx-1));
    document.getElementById('nextBtn').addEventListener('click',()=> show(idx+1));

    // keyboard
    window.addEventListener('keydown', (e)=>{
      if(e.key === 'ArrowRight' || e.key === 'PageDown') show(idx+1);
      if(e.key === 'ArrowLeft' || e.key === 'PageUp') show(idx-1);
    });

    // swipe support for touch
    let touchstartX = 0, touchendX = 0;
    const deck = document.getElementById('deck');
    deck.addEventListener('touchstart', e => touchstartX = e.changedTouches[0].screenX, false);
    deck.addEventListener('touchend', e => {
      touchendX = e.changedTouches[0].screenX;
      if(touchendX < touchstartX - 30) show(idx+1);
      if(touchendX > touchstartX + 30) show(idx-1);
    }, false);

    // init
    show(0);

    // optional: deep-link slide by #hash (e.g., #slide=3)
    const hash = location.hash.match(/slide=(\d+)/);
    if(hash) show(Math.max(0, Math.min(total-1, parseInt(hash[1],10)-1)));
  })();
</script>

</body>
</html>
