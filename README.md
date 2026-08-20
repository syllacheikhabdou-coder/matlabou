<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Matlabou Chifahi BIO — Prototype</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,700;1,9..144,500&family=Work+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --green-deep:#1F3A2E;
    --green-med:#2F5B44;
    --green-leaf:#4C8A66;
    --gold:#B8863B;
    --gold-soft:#E4C583;
    --kraft:#EFEAD9;
    --paper:#FBF9F2;
    --ink:#211F1A;
    --ink-soft:#5B594F;
    --line:#DCD5BE;
    --white:#FFFFFF;
    --red:#B24A3C;
    --radius:14px;
    --shadow: 0 10px 30px rgba(31,58,46,0.10);
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:'Work Sans', sans-serif;
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3,.display{
    font-family:'Fraunces', serif;
    color:var(--green-deep);
    margin:0;
  }
  .app{
    max-width:1180px;
    margin:0 auto;
    min-height:100vh;
    background:var(--paper);
    position:relative;
  }

  /* ---------- Barre de mode (Client / Interne) ---------- */
  .mode-switch{
    display:flex;
    justify-content:center;
    gap:0;
    background:var(--green-deep);
    padding:10px;
  }
  .mode-btn{
    border:none;
    background:transparent;
    color:#D8E3D5;
    font-family:'Work Sans',sans-serif;
    font-weight:600;
    font-size:13px;
    letter-spacing:0.06em;
    text-transform:uppercase;
    padding:10px 22px;
    border-radius:999px;
    cursor:pointer;
    transition:all .25s ease;
  }
  .mode-btn.active{
    background:var(--gold);
    color:var(--green-deep);
  }

  /* ---------- HEADER CLIENT ---------- */
  .topbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:22px 32px 16px;
    border-bottom:1px solid var(--line);
  }
  .brand{
    display:flex;
    align-items:center;
    gap:12px;
  }
  .leaf-mark{ width:34px; height:34px; }
  .brand-name{ font-size:22px; font-weight:700; letter-spacing:0.01em; line-height:1;}
  .brand-tag{ font-size:11px; color:var(--ink-soft); letter-spacing:0.08em; text-transform:uppercase; margin-top:3px;}
  .nav-links{ display:flex; gap:28px; }
  .nav-links a{ color:var(--green-deep); text-decoration:none; font-weight:500; font-size:14px; }
  .top-actions{ display:flex; align-items:center; gap:16px; }
  .icon-btn{
    position:relative;
    width:40px;height:40px;
    border-radius:999px;
    border:1px solid var(--line);
    background:var(--white);
    display:flex;align-items:center;justify-content:center;
    cursor:pointer;
  }
  .badge{
    position:absolute; top:-6px; right:-6px;
    background:var(--red); color:white; font-size:10px; font-weight:700;
    width:18px;height:18px;border-radius:50%;
    display:flex;align-items:center;justify-content:center;
  }

  /* ---------- HERO ---------- */
  .hero{
    display:flex; align-items:center; gap:40px;
    padding:44px 32px 30px;
  }
  .hero-copy{ flex:1.1; }
  .eyebrow{
    display:inline-flex; align-items:center; gap:8px;
    font-size:11px; letter-spacing:0.12em; text-transform:uppercase;
    color:var(--gold); font-weight:700; margin-bottom:14px;
  }
  .eyebrow::before{ content:""; width:18px; height:1px; background:var(--gold); display:inline-block;}
  .hero h1{ font-size:40px; line-height:1.08; font-weight:600; max-width:520px;}
  .hero p{ color:var(--ink-soft); margin-top:16px; max-width:440px; line-height:1.6; font-size:15px;}
  .hero-actions{ margin-top:26px; display:flex; gap:14px;}
  .btn-primary{
    background:var(--green-deep); color:var(--white); border:none;
    padding:13px 24px; border-radius:999px; font-weight:600; font-size:14px; cursor:pointer;
  }
  .btn-ghost{
    background:transparent; color:var(--green-deep); border:1px solid var(--green-deep);
    padding:13px 24px; border-radius:999px; font-weight:600; font-size:14px; cursor:pointer;
  }
  .hero-visual{
    flex:1; height:260px; border-radius:22px;
    background:
      radial-gradient(circle at 30% 20%, rgba(184,134,59,0.35), transparent 55%),
      linear-gradient(135deg, var(--green-deep), var(--green-med) 60%, var(--green-leaf));
    position:relative; overflow:hidden;
    display:flex; align-items:center; justify-content:center;
  }
  .hero-visual svg{ width:70%; opacity:0.9; }

  /* ---------- CATEGORY CHIPS ---------- */
  .chips{ display:flex; gap:10px; padding:0 32px 18px; flex-wrap:wrap; }
  .chip{
    padding:8px 16px; border-radius:999px; border:1px solid var(--line);
    font-size:13px; font-weight:500; color:var(--ink-soft); background:var(--white);
    cursor:pointer;
  }
  .chip.active{ background:var(--green-deep); color:white; border-color:var(--green-deep); }

  /* ---------- PRODUCT GRID ---------- */
  .section-title{
    display:flex; align-items:baseline; justify-content:space-between;
    padding:6px 32px 14px;
  }
  .section-title h2{ font-size:22px; font-weight:600; }
  .section-title span{ font-size:12px; color:var(--ink-soft); }
  .grid{
    display:grid; grid-template-columns:repeat(4,1fr); gap:18px;
    padding:0 32px 40px;
  }
  .card{
    background:var(--white); border:1px solid var(--line); border-radius:var(--radius);
    overflow:hidden; cursor:pointer; transition:transform .2s ease, box-shadow .2s ease;
  }
  .card:hover{ transform:translateY(-3px); box-shadow:var(--shadow); }
  .card-img{
    height:120px; display:flex; align-items:center; justify-content:center;
    font-size:38px;
  }
  .card-body{ padding:14px 14px 16px; }
  .card-cat{ font-size:10px; text-transform:uppercase; letter-spacing:0.08em; color:var(--gold); font-weight:700; }
  .card-name{ font-size:15px; font-weight:600; margin:5px 0 4px; color:var(--green-deep); }
  .card-desc{ font-size:12px; color:var(--ink-soft); line-height:1.4; min-height:32px; }
  .card-foot{ display:flex; align-items:center; justify-content:space-between; margin-top:10px; }
  .price{ font-weight:700; color:var(--ink); font-size:14px; }
  .add-btn{
    width:30px;height:30px;border-radius:50%; border:none; background:var(--green-deep);
    color:white; font-size:16px; cursor:pointer; display:flex; align-items:center; justify-content:center;
  }
  .stock-tag{ font-size:10px; color:var(--green-leaf); font-weight:600; }
  .stock-tag.low{ color:var(--red); }

  /* ---------- CART DRAWER ---------- */
  .drawer-overlay{
    position:fixed; inset:0; background:rgba(31,58,46,0.35);
    opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:40;
  }
  .drawer-overlay.open{ opacity:1; pointer-events:all; }
  .drawer{
    position:fixed; top:0; right:-380px; width:360px; height:100%;
    background:var(--paper); box-shadow:-10px 0 30px rgba(0,0,0,0.15);
    transition:right .3s ease; z-index:41; display:flex; flex-direction:column;
  }
  .drawer.open{ right:0; }
  .drawer-head{ padding:20px 22px; border-bottom:1px solid var(--line); display:flex; justify-content:space-between; align-items:center;}
  .drawer-items{ flex:1; overflow-y:auto; padding:14px 22px; }
  .cart-item{ display:flex; gap:12px; padding:12px 0; border-bottom:1px solid var(--line); align-items:center;}
  .cart-item-img{ width:42px;height:42px;border-radius:10px;background:var(--kraft); display:flex;align-items:center;justify-content:center; font-size:18px;}
  .cart-item-info{ flex:1; }
  .cart-item-info .name{ font-size:13px; font-weight:600; }
  .cart-item-info .qty{ font-size:12px; color:var(--ink-soft); }
  .drawer-foot{ padding:18px 22px; border-top:1px solid var(--line); background:var(--white); }
  .row-total{ display:flex; justify-content:space-between; font-weight:700; margin-bottom:14px; }
  .pay-options{ display:flex; gap:8px; margin-bottom:14px; }
  .pay-chip{ flex:1; border:1px solid var(--line); border-radius:10px; padding:8px; text-align:center; font-size:11px; font-weight:600; cursor:pointer; color:var(--ink-soft);}
  .pay-chip.active{ border-color:var(--gold); background:#FBF3E3; color:var(--gold); }
  .close-x{ background:none;border:none;font-size:18px;cursor:pointer;color:var(--ink-soft);}

  /* ---------- CHAT BUBBLE ---------- */
  .chat-bubble{
    position:fixed; bottom:26px; right:26px; width:56px;height:56px; border-radius:50%;
    background:var(--gold); color:var(--green-deep); border:none; box-shadow:var(--shadow);
    display:flex; align-items:center; justify-content:center; cursor:pointer; z-index:35; font-size:22px;
  }
  .chat-panel{
    position:fixed; bottom:94px; right:26px; width:320px; height:410px;
    background:var(--white); border-radius:18px; box-shadow:var(--shadow);
    display:flex; flex-direction:column; overflow:hidden; z-index:36;
    transform:translateY(16px); opacity:0; pointer-events:none; transition:all .25s ease;
  }
  .chat-panel.open{ transform:translateY(0); opacity:1; pointer-events:all; }
  .chat-head{ background:var(--green-deep); color:white; padding:14px 16px; display:flex; align-items:center; gap:10px;}
  .chat-head .dot{ width:8px;height:8px;border-radius:50%;background:#7FE3A6;}
  .chat-body{ flex:1; padding:14px; overflow-y:auto; display:flex; flex-direction:column; gap:10px; background:var(--kraft); }
  .msg{ max-width:78%; padding:9px 12px; border-radius:14px; font-size:13px; line-height:1.4; }
  .msg.them{ background:white; align-self:flex-start; border-bottom-left-radius:4px; }
  .msg.me{ background:var(--green-deep); color:white; align-self:flex-end; border-bottom-right-radius:4px; }
  .chat-input{ display:flex; border-top:1px solid var(--line); }
  .chat-input input{ flex:1; border:none; padding:12px; font-size:13px; font-family:inherit; outline:none;}
  .chat-input button{ background:var(--gold); border:none; padding:0 16px; cursor:pointer; font-weight:700; color:var(--green-deep);}

  /* ================= ESPACE INTERNE ================= */
  .internal{ display:none; }
  .internal.active{ display:block; }
  .client{ display:none; }
  .client.active{ display:block; }

  .int-header{
    display:flex; justify-content:space-between; align-items:center;
    padding:20px 32px; border-bottom:1px solid var(--line);
    background:var(--green-deep); color:white;
  }
  .int-header .brand-name{ color:white; }
  .int-header .brand-tag{ color:#BFD3C6; }
  .user-pill{
    display:flex; align-items:center; gap:10px; background:rgba(255,255,255,0.1);
    padding:6px 14px 6px 6px; border-radius:999px; font-size:13px;
  }
  .avatar{ width:28px;height:28px; border-radius:50%; background:var(--gold); color:var(--green-deep); font-weight:700; font-size:12px; display:flex;align-items:center;justify-content:center;}

  .int-tabs{ display:flex; gap:6px; padding:16px 32px 0; border-bottom:1px solid var(--line); background:var(--white);}
  .int-tab{
    padding:12px 18px; font-size:14px; font-weight:600; color:var(--ink-soft); cursor:pointer;
    border-bottom:2px solid transparent; display:flex; align-items:center; gap:8px;
  }
  .int-tab.active{ color:var(--green-deep); border-bottom-color:var(--gold); }

  .int-view{ display:none; padding:26px 32px 50px; }
  .int-view.active{ display:block; }

  .stat-row{ display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-bottom:24px;}
  .stat-card{ background:var(--white); border:1px solid var(--line); border-radius:var(--radius); padding:16px 18px;}
  .stat-card .label{ font-size:11px; text-transform:uppercase; letter-spacing:0.06em; color:var(--ink-soft); font-weight:600;}
  .stat-card .value{ font-family:'Fraunces',serif; font-size:26px; color:var(--green-deep); margin-top:6px;}
  .stat-card .delta{ font-size:11px; color:var(--green-leaf); font-weight:600; margin-top:4px;}
  .stat-card .delta.down{ color:var(--red); }

  /* POS layout */
  .pos-layout{ display:flex; gap:20px; }
  .pos-products{ flex:1.6; display:grid; grid-template-columns:repeat(3,1fr); gap:12px; align-content:start;}
  .pos-card{
    background:var(--white); border:1px solid var(--line); border-radius:12px; padding:12px; cursor:pointer; text-align:center;
    transition:border-color .15s ease;
  }
  .pos-card:hover{ border-color:var(--gold); }
  .pos-card .emoji{ font-size:26px; }
  .pos-card .nm{ font-size:12.5px; font-weight:600; margin-top:6px; color:var(--green-deep); }
  .pos-card .pr{ font-size:11px; color:var(--ink-soft); margin-top:2px;}

  .ticket{
    flex:1; background:var(--white); border:1px solid var(--line); border-radius:var(--radius);
    display:flex; flex-direction:column; height:fit-content; position:sticky; top:20px;
  }
  .ticket-head{ padding:16px 18px; border-bottom:1px dashed var(--line); font-weight:700; color:var(--green-deep);}
  .ticket-items{ padding:10px 18px; min-height:120px; max-height:260px; overflow-y:auto;}
  .ticket-row{ display:flex; justify-content:space-between; font-size:13px; padding:7px 0; border-bottom:1px solid #F1EEDF; }
  .ticket-empty{ color:var(--ink-soft); font-size:13px; text-align:center; padding:30px 0;}
  .ticket-total{ display:flex; justify-content:space-between; padding:14px 18px; font-weight:700; border-top:1px dashed var(--line); font-size:15px;}
  .pay-row{ display:flex; gap:8px; padding:0 18px 18px; }
  .pay-btn{ flex:1; border:1px solid var(--line); border-radius:10px; padding:10px 6px; font-size:12px; font-weight:600; background:var(--white); cursor:pointer; color:var(--ink-soft);}
  .pay-btn.gold{ background:var(--gold); color:white; border-color:var(--gold);}
  .validate-btn{ margin:0 18px 18px; background:var(--green-deep); color:white; border:none; padding:12px; border-radius:10px; font-weight:700; cursor:pointer;}

  /* Stock table */
  .stock-table{ width:100%; border-collapse:collapse; background:var(--white); border-radius:var(--radius); overflow:hidden; border:1px solid var(--line);}
  .stock-table th{ text-align:left; font-size:11px; text-transform:uppercase; letter-spacing:0.05em; color:var(--ink-soft); background:var(--kraft); padding:12px 16px; }
  .stock-table td{ padding:13px 16px; font-size:13.5px; border-top:1px solid var(--line); }
  .leaf-bar{ display:flex; gap:3px; }
  .leaf{ width:8px; height:14px; border-radius:3px 3px 3px 0; background:var(--line); }
  .leaf.filled{ background:var(--green-leaf); }
  .leaf.warn.filled{ background:var(--gold); }
  .leaf.crit.filled{ background:var(--red); }
  .tag{ font-size:10.5px; font-weight:700; padding:4px 9px; border-radius:999px; }
  .tag.ok{ background:#E6F2E9; color:var(--green-leaf); }
  .tag.warn{ background:#FBF0DA; color:var(--gold); }
  .tag.crit{ background:#F9E4E0; color:var(--red); }

  /* Orders */
  .order-row{ display:flex; align-items:center; justify-content:space-between; background:var(--white); border:1px solid var(--line); border-radius:12px; padding:14px 18px; margin-bottom:10px;}
  .order-left{ display:flex; gap:14px; align-items:center;}
  .order-id{ font-weight:700; color:var(--green-deep); font-size:14px;}
  .order-meta{ font-size:12px; color:var(--ink-soft); margin-top:2px;}
  select.status{
    border:1px solid var(--line); border-radius:8px; padding:7px 10px; font-size:12.5px; font-family:inherit; color:var(--ink);
  }

  @media (max-width:900px){
    .grid{ grid-template-columns:repeat(2,1fr); }
    .hero{ flex-direction:column; }
    .stat-row{ grid-template-columns:repeat(2,1fr); }
    .pos-layout{ flex-direction:column; }
    .pos-products{ grid-template-columns:repeat(2,1fr); }
    .nav-links{ display:none; }
  }
</style>
</head>
<body>
<div class="app">

  <div class="mode-switch">
    <button class="mode-btn active" id="btn-client" onclick="setMode('client')">Espace client</button>
    <button class="mode-btn" id="btn-internal" onclick="setMode('internal')">Espace interne</button>
  </div>

  <!-- ===================== ESPACE CLIENT ===================== -->
  <div class="client active" id="view-client">

    <div class="topbar">
      <div class="brand">
        <svg class="leaf-mark" viewBox="0 0 40 40" fill="none">
          <path d="M20 4C10 4 5 14 5 22C5 30 12 36 20 36C28 36 35 30 35 22C35 14 30 4 20 4Z" fill="#1F3A2E"/>
          <path d="M20 8V32M20 8C14 12 12 18 12 24M20 8C26 12 28 18 28 24" stroke="#E4C583" stroke-width="1.4" fill="none" stroke-linecap="round"/>
        </svg>
        <div>
          <div class="brand-name">Matlabou Chifahi BIO</div>
          <div class="brand-tag">Plantes médicinales</div>
        </div>
      </div>
      <div class="nav-links">
        <a href="#">Boutique</a>
        <a href="#">Nos plantes</a>
        <a href="#">Conseils</a>
        <a href="#">Mon compte</a>
      </div>
      <div class="top-actions">
        <button class="icon-btn" title="Compte">👤</button>
        <button class="icon-btn" onclick="openCart()" title="Panier">
          🧺 <span class="badge" id="cart-count">0</span>
        </button>
      </div>
    </div>

    <div class="hero">
      <div class="hero-copy">
        <div class="eyebrow">Récolte & transformation artisanale</div>
        <h1>Des plantes médicinales préparées avec soin, livrées près de chez vous</h1>
        <p>Tisanes, poudres et huiles issues de nos filières locales. Commandez en ligne, payez par Mobile Money, et échangez directement avec notre équipe pour un conseil personnalisé.</p>
        <div class="hero-actions">
          <button class="btn-primary" onclick="document.getElementById('grid').scrollIntoView({behavior:'smooth'})">Voir la boutique</button>
          <button class="btn-ghost" onclick="toggleChat(true)">Parler à un conseiller</button>
        </div>
      </div>
      <div class="hero-visual">
        <svg viewBox="0 0 200 140" fill="none">
          <ellipse cx="100" cy="120" rx="70" ry="10" fill="rgba(0,0,0,0.15)"/>
          <path d="M100 20C70 40 60 80 100 120C140 80 130 40 100 20Z" fill="#E4C583" opacity="0.9"/>
          <path d="M100 25V115" stroke="#1F3A2E" stroke-width="2"/>
          <path d="M100 45C85 55 80 70 80 85M100 45C115 55 120 70 120 85" stroke="#1F3A2E" stroke-width="2" fill="none"/>
        </svg>
      </div>
    </div>

    <div class="chips" id="chips"></div>

    <div class="section-title">
      <h2>Notre boutique</h2>
      <span id="grid-count">8 produits</span>
    </div>
    <div class="grid" id="grid"></div>
  </div>

  <!-- Cart Drawer -->
  <div class="drawer-overlay" id="overlay" onclick="closeCart()"></div>
  <div class="drawer" id="drawer">
    <div class="drawer-head">
      <h3 style="font-size:18px;">Mon panier</h3>
      <button class="close-x" onclick="closeCart()">✕</button>
    </div>
    <div class="drawer-items" id="drawer-items"></div>
    <div class="drawer-foot">
      <div class="row-total"><span>Total</span><span id="cart-total">0 FCFA</span></div>
      <div style="font-size:12px;color:var(--ink-soft);margin-bottom:8px;font-weight:600;">Paiement Mobile Money</div>
      <div class="pay-options">
        <div class="pay-chip active" data-pay="orange" onclick="selectPay(this)">Orange Money</div>
        <div class="pay-chip" data-pay="wave" onclick="selectPay(this)">Wave</div>
        <div class="pay-chip" data-pay="free" onclick="selectPay(this)">Free Money</div>
      </div>
      <button class="btn-primary" style="width:100%;" onclick="checkout()">Payer & confirmer la commande</button>
    </div>
  </div>

  <!-- Chat -->
  <button class="chat-bubble" onclick="toggleChat()">💬</button>
  <div class="chat-panel" id="chat-panel">
    <div class="chat-head">
      <div class="dot"></div>
      <div>
        <div style="font-weight:700;font-size:13px;">Matlabou Chifahi BIO</div>
        <div style="font-size:11px;color:#BFD3C6;">En ligne — répond sous 5 min</div>
      </div>
    </div>
    <div class="chat-body" id="chat-body">
      <div class="msg them">Bonjour 🌿 Comment pouvons-nous vous aider aujourd'hui ?</div>
      <div class="msg me">Bonjour, la tisane Kinkéliba est-elle disponible ?</div>
      <div class="msg them">Oui, elle est en stock. Vous voulez qu'on vous l'ajoute à votre panier ?</div>
    </div>
    <div class="chat-input">
      <input type="text" placeholder="Écrire un message..." id="chat-input-field">
      <button onclick="sendMsg()">Envoyer</button>
    </div>
  </div>

  <!-- ===================== ESPACE INTERNE ===================== -->
  <div class="internal" id="view-internal">
    <div class="int-header">
      <div class="brand">
        <svg class="leaf-mark" viewBox="0 0 40 40" fill="none">
          <path d="M20 4C10 4 5 14 5 22C5 30 12 36 20 36C28 36 35 30 35 22C35 14 30 4 20 4Z" fill="#E4C583"/>
          <path d="M20 8V32M20 8C14 12 12 18 12 24M20 8C26 12 28 18 28 24" stroke="#1F3A2E" stroke-width="1.4" fill="none" stroke-linecap="round"/>
        </svg>
        <div>
          <div class="brand-name">Espace interne</div>
          <div class="brand-tag">Caisse & gestion de stock</div>
        </div>
      </div>
      <div class="user-pill"><div class="avatar">FA</div> Fatou — Vendeuse</div>
    </div>

    <div class="int-tabs">
      <div class="int-tab active" onclick="setIntTab('pos', this)">🧾 Caisse</div>
      <div class="int-tab" onclick="setIntTab('stock', this)">🌿 Stock</div>
      <div class="int-tab" onclick="setIntTab('orders', this)">📦 Commandes en ligne</div>
      <div class="int-tab" onclick="setIntTab('stats', this)">📊 Statistiques</div>
    </div>

    <!-- POS -->
    <div class="int-view active" id="int-pos">
      <div class="pos-layout">
        <div class="pos-products" id="pos-products"></div>
        <div class="ticket">
          <div class="ticket-head">Ticket en cours</div>
          <div class="ticket-items" id="ticket-items">
            <div class="ticket-empty">Sélectionnez un produit pour commencer la vente</div>
          </div>
          <div class="ticket-total"><span>Total</span><span id="ticket-total">0 FCFA</span></div>
          <div class="pay-row">
            <button class="pay-btn" onclick="setPosPay(this,'especes')">Espèces</button>
            <button class="pay-btn gold" onclick="setPosPay(this,'mobile')">Mobile Money</button>
          </div>
          <button class="validate-btn" onclick="validateSale()">Encaisser la vente</button>
        </div>
      </div>
    </div>

    <!-- STOCK -->
    <div class="int-view" id="int-stock">
      <div class="stat-row">
        <div class="stat-card"><div class="label">Références actives</div><div class="value">8</div></div>
        <div class="stat-card"><div class="label">Alertes stock bas</div><div class="value" style="color:#B24A3C;">2</div></div>
        <div class="stat-card"><div class="label">Valeur du stock</div><div class="value">1,84 M</div><div class="delta">FCFA</div></div>
        <div class="stat-card"><div class="label">Mouvements (7j)</div><div class="value">34</div></div>
      </div>
      <table class="stock-table">
        <thead><tr><th>Produit</th><th>Catégorie</th><th>Stock</th><th>Niveau</th><th>Statut</th></tr></thead>
        <tbody id="stock-body"></tbody>
      </table>
    </div>

    <!-- ORDERS -->
    <div class="int-view" id="int-orders">
      <div id="orders-list"></div>
    </div>

    <!-- STATS -->
    <div class="int-view" id="int-stats">
      <div class="stat-row">
        <div class="stat-card"><div class="label">Ventes du jour</div><div class="value">142 000</div><div class="delta">+12% vs hier</div></div>
        <div class="stat-card"><div class="label">Ventes en ligne</div><div class="value">63 500</div><div class="delta">+8%</div></div>
        <div class="stat-card"><div class="label">Ventes boutique</div><div class="value">78 500</div><div class="delta">+15%</div></div>
        <div class="stat-card"><div class="label">Panier moyen</div><div class="value">4 750</div><div class="delta down">-3%</div></div>
      </div>
      <div class="section-title" style="padding:0 0 12px;"><h2 style="font-size:18px;">Produits les plus vendus</h2></div>
      <table class="stock-table">
        <thead><tr><th>Produit</th><th>Unités vendues (7j)</th><th>Chiffre d'affaires</th></tr></thead>
        <tbody>
          <tr><td>Tisane Kinkéliba</td><td>86</td><td>129 000 FCFA</td></tr>
          <tr><td>Huile de Moringa</td><td>54</td><td>162 000 FCFA</td></tr>
          <tr><td>Poudre de Baobab</td><td>47</td><td>94 000 FCFA</td></tr>
          <tr><td>Tisane Bissap-Gingembre</td><td>41</td><td>61 500 FCFA</td></tr>
        </tbody>
      </table>
    </div>
  </div>

</div>

<script>
const products = [
  {id:1, name:"Tisane Kinkéliba", cat:"Tisanes", price:1500, desc:"Digestive & détox, feuilles séchées", emoji:"🍵", stock:5, stockMax:40, alert:"crit"},
  {id:2, name:"Huile de Moringa", cat:"Huiles", price:3000, desc:"Pression à froid, peau & cheveux", emoji:"🧴", stock:22, stockMax:30, alert:"ok"},
  {id:3, name:"Poudre de Baobab", cat:"Poudres", price:2000, desc:"Riche en vitamine C, à diluer", emoji:"🥣", stock:14, stockMax:35, alert:"warn"},
  {id:4, name:"Tisane Bissap-Gingembre", cat:"Tisanes", price:1500, desc:"Antioxydant, tonique", emoji:"🌺", stock:31, stockMax:40, alert:"ok"},
  {id:5, name:"Poudre de Moringa", cat:"Poudres", price:2500, desc:"Complément nutritionnel quotidien", emoji:"🥬", stock:9, stockMax:30, alert:"warn"},
  {id:6, name:"Huile de Neem", cat:"Huiles", price:3500, desc:"Usage cutané, répulsif naturel", emoji:"🌿", stock:18, stockMax:25, alert:"ok"},
  {id:7, name:"Tisane Citronnelle-Menthe", cat:"Tisanes", price:1500, desc:"Relaxante, digestion", emoji:"🍃", stock:3, stockMax:40, alert:"crit"},
  {id:8, name:"Gélules Gingembre", cat:"Compléments", price:4000, desc:"Anti-inflammatoire naturel", emoji:"💊", stock:26, stockMax:30, alert:"ok"},
];

const cats = ["Tous", ...new Set(products.map(p=>p.cat))];
let activeCat = "Tous";
let cart = [];

function renderChips(){
  document.getElementById('chips').innerHTML = cats.map(c =>
    `<div class="chip ${c===activeCat?'active':''}" onclick="filterCat('${c}')">${c}</div>`
  ).join('');
}
function filterCat(c){ activeCat = c; renderChips(); renderGrid(); }

function renderGrid(){
  const list = activeCat==="Tous" ? products : products.filter(p=>p.cat===activeCat);
  document.getElementById('grid-count').textContent = list.length + " produits";
  document.getElementById('grid').innerHTML = list.map(p => `
    <div class="card">
      <div class="card-img" style="background:linear-gradient(135deg,#EFEAD9,#E4C583aa);">${p.emoji}</div>
      <div class="card-body">
        <div class="card-cat">${p.cat}</div>
        <div class="card-name">${p.name}</div>
        <div class="card-desc">${p.desc}</div>
        <div class="card-foot">
          <div>
            <div class="price">${p.price.toLocaleString()} FCFA</div>
            <div class="stock-tag ${p.stock<10?'low':''}">${p.stock<10?'Stock limité':'En stock'}</div>
          </div>
          <button class="add-btn" onclick="addToCart(${p.id})">+</button>
        </div>
      </div>
    </div>
  `).join('');
}

function addToCart(id){
  const p = products.find(x=>x.id===id);
  const existing = cart.find(x=>x.id===id);
  if(existing){ existing.qty++; } else { cart.push({...p, qty:1}); }
  renderCart();
  openCart();
}
function changeQty(id, delta){
  const item = cart.find(x=>x.id===id);
  item.qty += delta;
  if(item.qty<=0) cart = cart.filter(x=>x.id!==id);
  renderCart();
}
function renderCart(){
  document.getElementById('cart-count').textContent = cart.reduce((s,i)=>s+i.qty,0);
  const items = document.getElementById('drawer-items');
  if(cart.length===0){
    items.innerHTML = `<div class="ticket-empty">Votre panier est vide</div>`;
  } else {
    items.innerHTML = cart.map(i => `
      <div class="cart-item">
        <div class="cart-item-img">${i.emoji}</div>
        <div class="cart-item-info">
          <div class="name">${i.name}</div>
          <div class="qty">${i.price.toLocaleString()} FCFA</div>
        </div>
        <div style="display:flex;align-items:center;gap:8px;">
          <button class="icon-btn" style="width:26px;height:26px;" onclick="changeQty(${i.id},-1)">–</button>
          <span style="font-size:13px;font-weight:600;">${i.qty}</span>
          <button class="icon-btn" style="width:26px;height:26px;" onclick="changeQty(${i.id},1)">+</button>
        </div>
      </div>
    `).join('');
  }
  const total = cart.reduce((s,i)=>s+i.qty*i.price,0);
  document.getElementById('cart-total').textContent = total.toLocaleString()+" FCFA";
}
function openCart(){ document.getElementById('drawer').classList.add('open'); document.getElementById('overlay').classList.add('open'); }
function closeCart(){ document.getElementById('drawer').classList.remove('open'); document.getElementById('overlay').classList.remove('open'); }
function selectPay(el){ document.querySelectorAll('.pay-chip').forEach(c=>c.classList.remove('active')); el.classList.add('active'); }
function checkout(){
  if(cart.length===0){ alert("Votre panier est vide."); return; }
  alert("Commande confirmée ✅\nUn lien de paiement Mobile Money a été envoyé (simulation).");
  cart = []; renderCart(); closeCart();
}

function toggleChat(forceOpen){
  const panel = document.getElementById('chat-panel');
  if(forceOpen){ panel.classList.add('open'); return; }
  panel.classList.toggle('open');
}
function sendMsg(){
  const field = document.getElementById('chat-input-field');
  if(!field.value.trim()) return;
  const body = document.getElementById('chat-body');
  body.innerHTML += `<div class="msg me">${field.value}</div>`;
  field.value='';
  body.scrollTop = body.scrollHeight;
  setTimeout(()=>{
    body.innerHTML += `<div class="msg them">Merci, on revient vers vous très vite 🌿</div>`;
    body.scrollTop = body.scrollHeight;
  },700);
}

/* ---------- Mode switch ---------- */
function setMode(mode){
  document.getElementById('view-client').classList.toggle('active', mode==='client');
  document.getElementById('view-internal').classList.toggle('active', mode==='internal');
  document.getElementById('btn-client').classList.toggle('active', mode==='client');
  document.getElementById('btn-internal').classList.toggle('active', mode==='internal');
}

/* ---------- Internal tabs ---------- */
function setIntTab(tab, el){
  document.querySelectorAll('.int-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  document.querySelectorAll('.int-view').forEach(v=>v.classList.remove('active'));
  document.getElementById('int-'+tab).classList.add('active');
}

/* ---------- POS ---------- */
let posTicket = [];
let posPay = 'mobile';
function renderPos(){
  document.getElementById('pos-products').innerHTML = products.map(p=>`
    <div class="pos-card" onclick="addToTicket(${p.id})">
      <div class="emoji">${p.emoji}</div>
      <div class="nm">${p.name}</div>
      <div class="pr">${p.price.toLocaleString()} FCFA</div>
    </div>
  `).join('');
}
function addToTicket(id){
  const p = products.find(x=>x.id===id);
  const existing = posTicket.find(x=>x.id===id);
  if(existing){ existing.qty++; } else { posTicket.push({...p, qty:1}); }
  renderTicket();
}
function renderTicket(){
  const el = document.getElementById('ticket-items');
  if(posTicket.length===0){
    el.innerHTML = `<div class="ticket-empty">Sélectionnez un produit pour commencer la vente</div>`;
  } else {
    el.innerHTML = posTicket.map(i=>`
      <div class="ticket-row"><span>${i.qty} × ${i.name}</span><span>${(i.qty*i.price).toLocaleString()} FCFA</span></div>
    `).join('');
  }
  const total = posTicket.reduce((s,i)=>s+i.qty*i.price,0);
  document.getElementById('ticket-total').textContent = total.toLocaleString()+" FCFA";
}
function setPosPay(el, val){
  document.querySelectorAll('.pay-btn').forEach(b=>b.classList.remove('gold'));
  el.classList.add('gold');
  posPay = val;
}
function validateSale(){
  if(posTicket.length===0){ alert("Aucun article dans le ticket."); return; }
  const total = posTicket.reduce((s,i)=>s+i.qty*i.price,0);
  alert(`Vente encaissée ✅\nTotal : ${total.toLocaleString()} FCFA\nMode : ${posPay==='mobile'?'Mobile Money':'Espèces'}\nLe stock a été mis à jour automatiquement.`);
  posTicket = [];
  renderTicket();
}

/* ---------- Stock table ---------- */
function renderStock(){
  document.getElementById('stock-body').innerHTML = products.map(p=>{
    const pct = Math.round((p.stock/p.stockMax)*5);
    let leafClass = p.alert==='crit' ? 'crit' : (p.alert==='warn' ? 'warn' : '');
    const leaves = Array.from({length:5}).map((_,i)=>`<div class="leaf ${leafClass} ${i<pct?'filled':''}"></div>`).join('');
    const tagLabel = p.alert==='crit' ? 'Rupture proche' : (p.alert==='warn' ? 'Stock bas' : 'Stock sain');
    return `<tr>
      <td>${p.emoji} ${p.name}</td>
      <td>${p.cat}</td>
      <td>${p.stock} unités</td>
      <td><div class="leaf-bar">${leaves}</div></td>
      <td><span class="tag ${p.alert}">${tagLabel}</span></td>
    </tr>`;
  }).join('');
}

/* ---------- Orders ---------- */
const orders = [
  {id:"CMD-1042", client:"Awa Diop", total:"7 500 FCFA", status:"preparation"},
  {id:"CMD-1041", client:"Moussa Ba", total:"12 000 FCFA", status:"expediee"},
  {id:"CMD-1040", client:"Fatou Sarr", total:"3 000 FCFA", status:"livree"},
  {id:"CMD-1039", client:"Ibrahima Ndiaye", total:"9 500 FCFA", status:"preparation"},
];
function renderOrders(){
  document.getElementById('orders-list').innerHTML = orders.map(o=>`
    <div class="order-row">
      <div class="order-left">
        <div>
          <div class="order-id">${o.id}</div>
          <div class="order-meta">${o.client} · ${o.total}</div>
        </div>
      </div>
      <select class="status">
        <option value="preparation" ${o.status==='preparation'?'selected':''}>En préparation</option>
        <option value="expediee" ${o.status==='expediee'?'selected':''}>Expédiée</option>
        <option value="livree" ${o.status==='livree'?'selected':''}>Livrée</option>
      </select>
    </div>
  `).join('');
}

/* ---------- Init ---------- */
renderChips();
renderGrid();
renderCart();
renderPos();
renderTicket();
renderStock();
renderOrders();
</script>
</body>
</html>
