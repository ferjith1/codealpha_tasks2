<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Relay — instant answers for your website</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#12151A;
    --ink-2:#1B2028;
    --ink-3:#232A34;
    --paper:#F5F1E8;
    --paper-2:#EBE4D2;
    --line:rgba(255,255,255,0.09);
    --line-light:rgba(20,20,20,0.12);
    --text:#E7E5DE;
    --text-dim:#8B9199;
    --ink-text:#1A1C20;
    --ink-text-dim:#5B5C55;
    --signal:#46D6C6;
    --signal-dark:#1E7A70;
    --warm:#FF8552;
    --accent-soft:rgba(70,214,198,0.12);
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Inter', sans-serif;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--ink);
    color:var(--text);
    font-family:var(--sans);
    line-height:1.6;
    -webkit-font-smoothing:antialiased;
  }
  a{color:inherit;}
  img,svg{display:block; max-width:100%;}
  .wrap{max-width:1160px; margin:0 auto; padding:0 32px;}
  @media (max-width:700px){ .wrap{padding:0 20px;} }

  /* focus visibility */
  a:focus-visible, button:focus-visible, input:focus-visible{
    outline:2px solid var(--signal); outline-offset:2px;
  }

  /* ---------- NAV ---------- */
  header.nav{
    position:sticky; top:0; z-index:50;
    background:rgba(18,21,26,0.85);
    backdrop-filter:blur(10px);
    border-bottom:1px solid var(--line);
  }
  .nav-inner{
    display:flex; align-items:center; justify-content:space-between;
    height:68px;
  }
  .logo{
    font-family:var(--mono); font-weight:700; font-size:18px;
    letter-spacing:0.02em; display:flex; align-items:center; gap:8px;
  }
  .logo .dot{width:8px; height:8px; border-radius:50%; background:var(--signal); box-shadow:0 0 0 3px var(--accent-soft);}
  .nav-links{display:flex; gap:32px; font-size:14px; color:var(--text-dim);}
  .nav-links a{text-decoration:none; transition:color .15s;}
  .nav-links a:hover{color:var(--text);}
  .nav-cta{
    font-family:var(--mono); font-size:13px; font-weight:500;
    background:var(--signal); color:#08201D;
    padding:9px 18px; border-radius:6px; text-decoration:none;
    border:none; cursor:pointer;
  }
  @media (max-width:780px){ .nav-links{display:none;} }

  /* ---------- HERO ---------- */
  .hero{padding:76px 0 64px;}
  .hero-grid{
    display:grid; grid-template-columns:1.05fr 0.95fr; gap:56px; align-items:start;
  }
  @media (max-width:920px){ .hero-grid{grid-template-columns:1fr;} }

  .eyebrow{
    font-family:var(--mono); font-size:12px; letter-spacing:0.12em; text-transform:uppercase;
    color:var(--signal); margin-bottom:20px; display:flex; align-items:center; gap:10px;
  }
  .eyebrow::before{content:''; width:16px; height:1px; background:var(--signal);}

  h1{
    font-family:var(--mono); font-weight:700;
    font-size:clamp(30px, 4.2vw, 46px);
    line-height:1.12; letter-spacing:-0.01em;
    color:#fff; margin-bottom:22px;
  }
  h1 .em{color:var(--signal);}

  .lede{font-size:17px; color:var(--text-dim); max-width:46ch; margin-bottom:32px;}

  .hero-ctas{display:flex; gap:14px; margin-bottom:44px; flex-wrap:wrap;}
  .btn-primary{
    font-family:var(--mono); font-size:14px; font-weight:500;
    background:var(--signal); color:#08201D; border:none;
    padding:13px 22px; border-radius:6px; cursor:pointer; text-decoration:none;
    display:inline-flex; align-items:center; gap:8px;
  }
  .btn-secondary{
    font-family:var(--mono); font-size:14px; font-weight:500;
    background:transparent; color:var(--text); border:1px solid var(--line);
    padding:13px 22px; border-radius:6px; cursor:pointer; text-decoration:none;
  }
  .btn-secondary:hover{border-color:var(--text-dim);}

  .stat-row{display:flex; gap:36px; flex-wrap:wrap;}
  .stat{}
  .stat b{font-family:var(--mono); font-size:22px; color:#fff; display:block;}
  .stat span{font-size:12px; color:var(--text-dim);}

  /* ---------- CHAT WIDGET ---------- */
  .widget{
    background:var(--ink-2); border:1px solid var(--line); border-radius:14px;
    overflow:hidden; display:flex; flex-direction:column; height:480px;
    box-shadow:0 30px 60px -30px rgba(0,0,0,0.6);
  }
  .widget-head{
    display:flex; align-items:center; gap:10px; padding:14px 18px;
    border-bottom:1px solid var(--line); background:var(--ink-3);
  }
  .widget-head .pulse{
    width:8px; height:8px; border-radius:50%; background:var(--signal);
    box-shadow:0 0 0 0 rgba(70,214,198,0.6); animation:pulse 2s infinite;
  }
  @media (prefers-reduced-motion:reduce){ .widget-head .pulse{animation:none;} }
  @keyframes pulse{
    0%{box-shadow:0 0 0 0 rgba(70,214,198,0.5);}
    70%{box-shadow:0 0 0 8px rgba(70,214,198,0);}
    100%{box-shadow:0 0 0 0 rgba(70,214,198,0);}
  }
  .widget-head span{font-size:13px; font-weight:500;}
  .widget-head small{margin-left:auto; font-family:var(--mono); font-size:11px; color:var(--text-dim);}

  .widget-body{flex:1; overflow-y:auto; padding:18px; display:flex; flex-direction:column; gap:12px;}
  .msg{max-width:82%; font-size:14px; padding:10px 13px; border-radius:10px; line-height:1.5;}
  .msg.bot{background:var(--ink-3); align-self:flex-start; border-bottom-left-radius:3px;}
  .msg.user{background:var(--signal); color:#08201D; align-self:flex-end; border-bottom-right-radius:3px;}
  .msg.bot .meta{display:block; margin-top:6px; font-family:var(--mono); font-size:10.5px; color:var(--text-dim);}

  .widget-foot{
    display:flex; gap:8px; padding:12px; border-top:1px solid var(--line); background:var(--ink-3);
  }
  .widget-foot input{
    flex:1; background:var(--ink); border:1px solid var(--line); border-radius:7px;
    padding:10px 12px; color:var(--text); font-family:var(--sans); font-size:14px;
  }
  .widget-foot input::placeholder{color:var(--text-dim);}
  .widget-foot button{
    background:var(--signal); border:none; border-radius:7px; padding:0 16px;
    color:#08201D; font-weight:600; cursor:pointer; font-family:var(--mono); font-size:13px;
  }
  .chip-row{display:flex; gap:8px; flex-wrap:wrap; padding:0 18px 14px;}
  .chip{
    font-family:var(--mono); font-size:11.5px; color:var(--text-dim);
    border:1px solid var(--line); border-radius:20px; padding:5px 11px; background:none;
    cursor:pointer;
  }
  .chip:hover{color:var(--text); border-color:var(--text-dim);}

  /* ---------- CONSOLE / SIGNATURE SECTION ---------- */
  .console-section{background:var(--paper); color:var(--ink-text); padding:80px 0;}
  .console-head{max-width:60ch; margin-bottom:40px;}
  .console-head .eyebrow{color:var(--signal-dark);}
  .console-head .eyebrow::before{background:var(--signal-dark);}
  .console-head h2{
    font-family:var(--mono); font-size:clamp(24px,3vw,32px); color:var(--ink-text);
    margin-bottom:14px; line-height:1.2;
  }
  .console-head p{color:var(--ink-text-dim); font-size:15.5px;}

  .console{
    background:var(--ink); border-radius:12px; padding:20px 22px;
    font-family:var(--mono); font-size:12.5px; height:280px; overflow-y:auto;
    border:1px solid var(--line);
  }
  .console .line{color:var(--text-dim); margin-bottom:7px; white-space:pre-wrap;}
  .console .line .tag-hit{color:var(--signal);}
  .console .line .tag-miss{color:var(--warm);}
  .console .line .prompt{color:#fff;}
  .console-empty{color:var(--text-dim);}

  /* ---------- INTENT LIBRARY ---------- */
  .intents-section{padding:84px 0; background:var(--ink);}
  .section-head{max-width:60ch; margin-bottom:44px;}
  .section-head h2{font-family:var(--mono); font-size:clamp(24px,3vw,32px); color:#fff; margin-bottom:14px;}
  .section-head p{color:var(--text-dim); font-size:15.5px;}

  .intent-grid{display:grid; grid-template-columns:repeat(4, 1fr); gap:16px;}
  @media (max-width:920px){ .intent-grid{grid-template-columns:repeat(2,1fr);} }
  @media (max-width:560px){ .intent-grid{grid-template-columns:1fr;} }
  .intent-card{
    background:var(--ink-2); border:1px solid var(--line); border-radius:10px; padding:18px;
  }
  .intent-card .name{font-family:var(--mono); font-size:13px; color:var(--signal); margin-bottom:10px;}
  .intent-card .phrases{display:flex; flex-wrap:wrap; gap:6px;}
  .intent-card .phrases span{
    font-size:11.5px; color:var(--text-dim); border:1px solid var(--line);
    border-radius:5px; padding:3px 7px;
  }

  /* ---------- INTEGRATION ---------- */
  .integrate-section{background:var(--paper-2); color:var(--ink-text); padding:84px 0;}
  .integrate-grid{display:grid; grid-template-columns:0.9fr 1.1fr; gap:48px; align-items:center;}
  @media (max-width:920px){ .integrate-grid{grid-template-columns:1fr;} }
  .integrate-grid h2{font-family:var(--mono); font-size:clamp(22px,2.8vw,30px); margin-bottom:16px;}
  .integrate-grid p{color:var(--ink-text-dim); font-size:15.5px; margin-bottom:14px;}
  .integrate-list{list-style:none; margin-top:18px;}
  .integrate-list li{
    display:flex; gap:10px; font-size:14px; color:var(--ink-text); margin-bottom:10px; align-items:flex-start;
  }
  .integrate-list li::before{content:'—'; color:var(--signal-dark); flex-shrink:0;}

  .code-block{
    background:var(--ink); border-radius:12px; overflow:hidden; border:1px solid var(--line);
  }
  .code-head{
    display:flex; align-items:center; justify-content:space-between;
    padding:10px 16px; border-bottom:1px solid var(--line); background:var(--ink-3);
  }
  .code-head span{font-family:var(--mono); font-size:12px; color:var(--text-dim);}
  .copy-btn{
    font-family:var(--mono); font-size:11.5px; background:none; color:var(--signal);
    border:1px solid var(--signal-dark); border-radius:5px; padding:5px 10px; cursor:pointer;
  }
  .code-block pre{
    padding:20px; font-family:var(--mono); font-size:12.5px; color:var(--text);
    overflow-x:auto; line-height:1.7;
  }
  .code-block .k{color:var(--signal);}
  .code-block .s{color:var(--warm);}

  /* ---------- METRICS ---------- */
  .metrics-section{padding:84px 0; background:var(--ink);}
  .metric-grid{display:grid; grid-template-columns:repeat(4,1fr); gap:18px;}
  @media (max-width:920px){ .metric-grid{grid-template-columns:repeat(2,1fr);} }
  @media (max-width:560px){ .metric-grid{grid-template-columns:1fr;} }
  .metric-card{
    background:var(--ink-2); border:1px solid var(--line); border-radius:10px; padding:22px;
  }
  .metric-card .label{font-family:var(--mono); font-size:12px; color:var(--text-dim); margin-bottom:14px;}
  .metric-card .value{font-family:var(--mono); font-size:26px; color:#fff; margin-bottom:12px;}
  .bar-track{height:5px; background:var(--ink-3); border-radius:3px; overflow:hidden;}
  .bar-fill{height:100%; background:var(--signal); border-radius:3px;}

  /* ---------- FOOTER ---------- */
  footer{border-top:1px solid var(--line); padding:36px 0;}
  .footer-inner{display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:16px;}
  footer .logo{font-size:15px;}
  footer .foot-links{display:flex; gap:24px; font-size:13px; color:var(--text-dim);}
  footer .foot-links a{text-decoration:none;}
  footer .foot-links a:hover{color:var(--text);}
</style>
</head>
<body>

<header class="nav">
  <div class="wrap nav-inner">
    <div class="logo"><span class="dot"></span>relay</div>
    <nav class="nav-links">
      <a href="#demo">Live demo</a>
      <a href="#intents">Intent library</a>
      <a href="#integrate">Integration</a>
      <a href="#metrics">Metrics</a>
    </nav>
    <button class="nav-cta" onclick="document.getElementById('demo').scrollIntoView()">Get a demo</button>
  </div>
</header>

<section class="hero">
  <div class="wrap hero-grid">
    <div>
      <div class="eyebrow">AI chatbot for websites</div>
      <h1>Answers arrive before the visitor<br>finishes reading the <span class="em">question.</span></h1>
      <p class="lede">Relay pairs a trained intent library with a generative fallback, so common questions get instant, exact answers and everything else still gets handled — never a dead end.</p>
      <div class="hero-ctas">
        <a class="btn-primary" href="#demo">Try the live demo →</a>
        <a class="btn-secondary" href="#integrate">View the embed code</a>
      </div>
      <div class="stat-row">
        <div class="stat"><b>&lt;80ms</b><span>median retrieval latency</span></div>
        <div class="stat"><b>94%</b><span>intent match accuracy</span></div>
        <div class="stat"><b>1 script tag</b><span>to integrate</span></div>
      </div>
    </div>

    <div id="demo" class="widget">
      <div class="widget-head">
        <span class="pulse"></span>
        <span>Relay assistant</span>
        <small id="widget-status">online</small>
      </div>
      <div class="widget-body" id="chat-body">
        <div class="msg bot">Hi, I'm the Relay assistant for this demo store. Ask about pricing, shipping, returns, or order tracking.</div>
      </div>
      <div class="chip-row">
        <button class="chip" data-q="What does it cost?">What does it cost?</button>
        <button class="chip" data-q="Where is my order?">Where is my order?</button>
        <button class="chip" data-q="Can I get a refund?">Can I get a refund?</button>
      </div>
      <div class="widget-foot">
        <input id="chat-input" type="text" placeholder="Type a question…" autocomplete="off">
        <button id="chat-send">Send</button>
      </div>
    </div>
  </div>
</section>

<section class="console-section">
  <div class="wrap">
    <div class="console-head">
      <div class="eyebrow">Confidence trace</div>
      <h2>Every message is scored, not guessed.</h2>
      <p>Type in the widget above and watch the decision engine here — intent matched, confidence score, and which path answered: retrieval or fallback.</p>
    </div>
    <div class="console" id="console-log">
      <div class="console-empty">// waiting for a message…</div>
    </div>
  </div>
</section>

<section class="intents-section" id="intents">
  <div class="wrap">
    <div class="section-head">
      <div class="eyebrow">Trained on your patterns</div>
      <h2>A commercial intent library, tuned per business</h2>
      <p>Each intent is trained on real phrasings your customers actually use, not just the textbook version of the question.</p>
    </div>
    <div class="intent-grid">
      <div class="intent-card">
        <div class="name">pricing_question</div>
        <div class="phrases"><span>how much is it</span><span>what's the cost</span><span>plans &amp; pricing</span></div>
      </div>
      <div class="intent-card">
        <div class="name">order_tracking</div>
        <div class="phrases"><span>where's my order</span><span>track my package</span><span>order status</span></div>
      </div>
      <div class="intent-card">
        <div class="name">returns_refunds</div>
        <div class="phrases"><span>can I return this</span><span>refund policy</span><span>exchange an item</span></div>
      </div>
      <div class="intent-card">
        <div class="name">shipping_info</div>
        <div class="phrases"><span>delivery time</span><span>do you ship internationally</span><span>shipping cost</span></div>
      </div>
    </div>
  </div>
</section>

<section class="integrate-section" id="integrate">
  <div class="wrap integrate-grid">
    <div>
      <h2>Drop it into any website</h2>
      <p>One script tag reads your brand colors, mounts the widget, and starts answering — no iframe wrangling, no backend rewrite.</p>
      <ul class="integrate-list">
        <li>Inherits your site's font and accent color automatically</li>
        <li>Works alongside your existing support tools; escalates to a human on request</li>
        <li>Session context passes through, so logged-in users get personalized answers</li>
      </ul>
    </div>
    <div class="code-block">
      <div class="code-head">
        <span>index.html</span>
        <button class="copy-btn" id="copy-snippet">Copy</button>
      </div>
      <pre>&lt;<span class="k">script</span>
  <span class="k">src</span>=<span class="s">"https://cdn.relay.chat/widget.js"</span>
  <span class="k">data-site</span>=<span class="s">"your-site-id"</span>
  <span class="k">data-accent</span>=<span class="s">"#46D6C6"</span>
  <span class="k">async</span>&gt;
&lt;/<span class="k">script</span>&gt;</pre>
    </div>
  </div>
</section>

<section class="metrics-section" id="metrics">
  <div class="wrap">
    <div class="section-head">
      <div class="eyebrow">Optimized continuously</div>
      <h2>Every escalation retrains the library</h2>
      <p>Questions that miss the intent library get logged, reviewed, and folded back in — so accuracy climbs the more the bot is used.</p>
    </div>
    <div class="metric-grid">
      <div class="metric-card">
        <div class="label">Intent match accuracy</div>
        <div class="value">94%</div>
        <div class="bar-track"><div class="bar-fill" style="width:94%"></div></div>
      </div>
      <div class="metric-card">
        <div class="label">Self-service resolution</div>
        <div class="value">78%</div>
        <div class="bar-track"><div class="bar-fill" style="width:78%"></div></div>
      </div>
      <div class="metric-card">
        <div class="label">Median response time</div>
        <div class="value">80ms</div>
        <div class="bar-track"><div class="bar-fill" style="width:88%"></div></div>
      </div>
      <div class="metric-card">
        <div class="label">Visitor satisfaction</div>
        <div class="value">4.6/5</div>
        <div class="bar-track"><div class="bar-fill" style="width:92%"></div></div>
      </div>
    </div>
  </div>
</section>

<footer>
  <div class="wrap footer-inner">
    <div class="logo"><span class="dot" style="display:inline-block;width:7px;height:7px;border-radius:50%;background:var(--signal);margin-right:8px;"></span>relay</div>
    <div class="foot-links">
      <a href="#demo">Live demo</a>
      <a href="#integrate">Integration</a>
      <a href="#metrics">Metrics</a>
    </div>
  </div>
</footer>

<script>
// ---- Intent library (predefined patterns for the retrieval demo) ----
const INTENTS = [
  {
    name: 'pricing_question',
    keywords: ['price','cost','pricing','plan','plans','much','expensive','fee','fees'],
    reply: "Relay starts at $49/mo for up to 2,000 conversations, with unlimited intents. Larger plans add seats and priority support."
  },
  {
    name: 'order_tracking',
    keywords: ['order','track','tracking','package','shipment','status','where'],
    reply: "I can pull that up once you share your order number — in this demo, order #10432 shipped yesterday and arrives Thursday."
  },
  {
    name: 'returns_refunds',
    keywords: ['return','refund','exchange','money','back','cancel'],
    reply: "Returns are accepted within 30 days of delivery for a full refund. Exchanges ship out the same day we receive your item."
  },
  {
    name: 'shipping_info',
    keywords: ['shipping','deliver','delivery','ship','international','arrive','long'],
    reply: "Standard shipping takes 3–5 business days domestically, 7–14 internationally. Free over $75."
  },
  {
    name: 'greeting',
    keywords: ['hi','hello','hey','morning','afternoon'],
    reply: "Hey! Ask me about pricing, shipping, returns, or an order — I'll do my best to help right away."
  }
];

const THRESHOLD = 0.32;

function scoreIntent(text, intent){
  const tokens = text.toLowerCase().replace(/[^a-z0-9\s]/g,'').split(/\s+/).filter(Boolean);
  if(tokens.length === 0) return 0;
  let hits = 0;
  tokens.forEach(t => { if(intent.keywords.includes(t)) hits++; });
  return hits / tokens.length;
}

function classify(text){
  let best = null, bestScore = 0;
  INTENTS.forEach(intent => {
    const s = scoreIntent(text, intent);
    if(s > bestScore){ bestScore = s; best = intent; }
  });
  return { intent: best, confidence: bestScore };
}

const chatBody = document.getElementById('chat-body');
const chatInput = document.getElementById('chat-input');
const chatSend = document.getElementById('chat-send');
const consoleLog = document.getElementById('console-log');
const widgetStatus = document.getElementById('widget-status');

function addMessage(text, who, meta){
  const el = document.createElement('div');
  el.className = 'msg ' + who;
  el.textContent = text;
  if(meta){
    const m = document.createElement('span');
    m.className = 'meta';
    m.textContent = meta;
    el.appendChild(m);
  }
  chatBody.appendChild(el);
  chatBody.scrollTop = chatBody.scrollHeight;
}

function logLine(html){
  const empty = consoleLog.querySelector('.console-empty');
  if(empty) empty.remove();
  const el = document.createElement('div');
  el.className = 'line';
  el.innerHTML = html;
  consoleLog.appendChild(el);
  consoleLog.scrollTop = consoleLog.scrollHeight;
}

function handleQuery(text){
  if(!text.trim()) return;
  addMessage(text, 'user');
  chatInput.value = '';
  widgetStatus.textContent = 'thinking…';

  const start = performance.now();
  const { intent, confidence } = classify(text);
  const latency = Math.round(28 + Math.random()*55);

  logLine(`<span class="prompt">&gt; "${escapeHtml(text)}"</span>`);

  setTimeout(() => {
    if(intent && confidence >= THRESHOLD){
      logLine(`  <span class="tag-hit">retrieval hit</span> — intent: ${intent.name}, confidence: ${confidence.toFixed(2)}, ${latency}ms`);
      addMessage(intent.reply, 'bot', `${intent.name} · ${(confidence*100).toFixed(0)}% confidence · ${latency}ms`);
    } else {
      logLine(`  <span class="tag-miss">fallback</span> — no intent above threshold (best: ${confidence.toFixed(2)}), routing to generative model, ${latency}ms`);
      addMessage("That's outside my trained patterns for this demo — in production this would route to the generative fallback (or a human) instead of a dead end.", 'bot', `fallback · ${latency}ms`);
    }
    widgetStatus.textContent = 'online';
  }, 260);
}

function escapeHtml(str){
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}

chatSend.addEventListener('click', () => handleQuery(chatInput.value));
chatInput.addEventListener('keydown', e => { if(e.key === 'Enter') handleQuery(chatInput.value); });
document.querySelectorAll('.chip').forEach(chip => {
  chip.addEventListener('click', () => handleQuery(chip.dataset.q));
});

// copy snippet
document.getElementById('copy-snippet').addEventListener('click', function(){
  const snippet = '<script src="https://cdn.relay.chat/widget.js" data-site="your-site-id" data-accent="#46D6C6" async><' + '/script>';
  navigator.clipboard.writeText(snippet).then(() => {
    this.textContent = 'Copied';
    setTimeout(() => this.textContent = 'Copy', 1600);
  });
});
</script>

</body>
</html>
