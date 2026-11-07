#   
<!DOCTYPE html>  
<html lang="fr">  
<head>  
  <meta charset="UTF-8" />  
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />  
  <meta name="apple-mobile-web-app-capable" content="yes" />  
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />  
  <title>HELIOS · v7.2 (Départ à zéro)</title>  
  <style>  
    :root {  
      --bg-base: #070b0a;  
      --bg-card: rgba(14, 21, 19, 0.88);  
      --bg-card-elevated: rgba(20, 30, 27, 0.94);  
      --border-subtle: rgba(255, 255, 255, 0.11);  
      --border-emerald: rgba(46, 213, 115, 0.35);  
      --border-alert: rgba(235, 77, 75, 0.5);  
      --border-cyan: rgba(56, 189, 248, 0.4);  
      --text-main: #f1f5f3;  
      --text-muted: #8fa39b;  
      --text-dim: #5c7068;  
      --emerald: #2ed573;  
      --emerald-bg: rgba(46, 213, 115, 0.15);  
      --ruby: #ff5252;  
      --ruby-bg: rgba(255, 82, 82, 0.16);  
      --amber: #ffa502;  
      --amber-bg: rgba(255, 165, 2, 0.16);  
      --cyan: #38bdf8;  
      --cyan-bg: rgba(56, 189, 248, 0.16);  
      --font-sans: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Inter", sans-serif;  
      --font-mono: "SF Mono", ui-monospace, Menlo, monospace;  
      --font-serif: "New York", Georgia, serif;  
    }  
  
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }  
    body {  
      background-color: var(--bg-base);  
      background-image:   
        radial-gradient(circle at 20% 0%, rgba(16, 52, 40, 0.35) 0%, transparent 55%),  
        radial-gradient(circle at 90% 100%, rgba(18, 42, 54, 0.25) 0%, transparent 50%);  
      color: var(--text-main);  
      font-family: var(--font-sans);  
      font-size: 15px;  
      line-height: 1.45;  
      min-height: 100vh;  
      padding-bottom: 140px;  
      overflow-x: hidden;  
    }  
  
    .app-header {  
      position: sticky; top: 0; z-index: 100;  
      background: rgba(7, 11, 10, 0.88);  
      backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);  
      padding: 12px 14px 10px; border-bottom: 1px solid var(--border-subtle);  
    }  
    .header-top-row { display: flex; align-items: center; justify-content: space-between; gap: 8px; margin-bottom: 10px; }  
    .pill-top-btn {  
      background: rgba(255, 255, 255, 0.04); border: 1px solid var(--border-subtle);  
      color: var(--text-main); border-radius: 999px; padding: 6px 12px; font-size: 11px;  
      letter-spacing: 0.08em; text-transform: uppercase; cursor: pointer; text-align: center;  
    }  
    .brand-title { font-family: var(--font-serif); font-size: 18px; letter-spacing: 0.28em; cursor: pointer; }  
      
    .ws-banner {  
      background: var(--bg-card); border: 1px solid var(--border-subtle);  
      border-radius: 22px; padding: 10px 14px; display: flex; align-items: center; justify-content: space-between; cursor: pointer;  
    }  
    .ws-left { display: flex; align-items: center; gap: 10px; }  
    .dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; }  
    .dot-grey { background: #6c7a75; }  
    .dot-green { background: var(--emerald); box-shadow: 0 0 8px var(--emerald); }  
    .dot-amber { background: var(--amber); box-shadow: 0 0 8px var(--amber); }  
  
    .td-drawer {  
      display: none; margin-top: 10px; background: var(--bg-card-elevated);  
      border: 1px solid var(--border-subtle); border-radius: 18px; padding: 14px; max-height: 70vh; overflow-y: auto;  
    }  
    .td-drawer.open { display: block; }  
    .td-table { width: 100%; border-collapse: collapse; margin-bottom: 14px; }  
    .td-table th { text-align: left; font-size: 11px; color: var(--text-muted); padding-bottom: 8px; border-bottom: 1px solid var(--border-subtle); }  
    .td-table td { padding: 8px 4px; border-bottom: 1px solid rgba(255, 255, 255, 0.06); font-size: 13px; }  
  
    .container { max-width: 600px; margin: 0 auto; padding: 18px 14px; }  
    .screen { display: none; }  
    .screen.active { display: block; }  
  
    .eyebrow { font-size: 11.5px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-muted); margin-bottom: 6px; }  
    .page-title { font-family: var(--font-serif); font-size: 28px; font-weight: 400; letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 14px; }  
    .section-label { font-size: 12px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-muted); margin: 20px 0 10px; }  
  
    .broker-badge { display: inline-flex; align-items: center; gap: 6px; padding: 5px 12px; border-radius: 999px; font-size: 12.5px; background: rgba(255, 255, 255, 0.05); border: 1px solid var(--border-subtle); color: var(--text-muted); margin-bottom: 14px; }  
    .broker-badge.cyan { background: var(--cyan-bg); border-color: var(--border-cyan); color: #bae6fd; }  
  
    .card { background: var(--bg-card); border: 1px solid var(--border-subtle); border-radius: 20px; padding: 16px; margin-bottom: 12px; }  
    .card-alert { border-color: var(--border-alert); background: rgba(42, 16, 16, 0.5); }  
    .card-header-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px; }  
    .mono-text { font-family: var(--font-mono); }  
  
    .tag { display: inline-block; padding: 3px 10px; border-radius: 999px; font-size: 12px; font-weight: 500; }  
    .tag-buy { background: var(--emerald-bg); color: var(--emerald); border: 1px solid var(--border-emerald); }  
    .tag-sell { background: var(--ruby-bg); color: var(--ruby); border: 1px solid var(--border-alert); }  
    .tag-wait { background: var(--cyan-bg); color: var(--cyan); border: 1px solid var(--border-cyan); }  
  
    .counter-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin: 14px 0; }  
    .counter-box { background: var(--bg-card); border: 1px solid var(--border-subtle); border-radius: 18px; padding: 12px; }  
    .counter-label { font-size: 10px; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text-muted); min-height: 26px; }  
    .counter-num { font-family: var(--font-serif); font-size: 30px; margin-top: 4px; }  
  
    .btn-block {  
      width: 100%; padding: 12px 16px; border-radius: 999px; border: 1px solid var(--border-subtle);  
      background: rgba(255, 255, 255, 0.03); color: var(--text-main); font-size: 12px;  
      letter-spacing: 0.1em; text-transform: uppercase; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 8px; margin-top: 10px;  
    }  
    .btn-block.emerald { border-color: var(--border-emerald); color: var(--emerald); background: var(--emerald-bg); font-weight: 600; }  
    .btn-block.danger { border-color: var(--border-alert); color: #ff9f9f; background: rgba(255, 82, 82, 0.08); }  
  
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }  
    .input-field { width: 100%; background: rgba(255, 255, 255, 0.04); border: 1px solid var(--border-subtle); border-radius: 14px; padding: 11px 14px; color: var(--text-main); font-size: 14px; margin-top: 8px; }  
  
    .bottom-nav {  
      position: fixed; bottom: 0; left: 0; right: 0; z-index: 100;  
      background: rgba(7, 11, 10, 0.94); backdrop-filter: blur(18px); -webkit-backdrop-filter: blur(18px);  
      border-top: 1px solid var(--border-subtle); display: grid; grid-template-columns: repeat(4, 1fr);  
      padding: 6px 8px calc(8px + env(safe-area-inset-bottom));  
    }  
    .nav-tab { display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 8px 4px; color: var(--text-muted); font-size: 12.5px; cursor: pointer; position: relative; }  
    .nav-tab.active { color: var(--text-main); font-weight: 600; }  
    .nav-tab.active::after { content: ""; position: absolute; bottom: 0; width: 42px; height: 2.5px; background: var(--text-main); border-radius: 2px; }  
  
    .fab-veille {  
      position: fixed; bottom: 74px; right: 14px; z-index: 95;  
      background: rgba(16, 25, 22, 0.95); border: 1px solid rgba(255, 255, 255, 0.22);  
      color: var(--text-main); padding: 11px 18px; border-radius: 999px; font-size: 13px; font-weight: 500; cursor: pointer;  
    }  
  </style>  
</head>  
<body>  
  
  <!-- TOP HEADER -->  
  <header class="app-header">  
    <div class="header-top-row">  
      <button class="pill-top-btn" onclick="switchScreen('journal')">JOURNAL /<br>CONTRÔLE</button>  
      <div class="brand-title" onclick="switchScreen('accueil')">HELIOS</div>  
      <button class="pill-top-btn" onclick="switchScreen('reglages')">☰ MENU ·<br>RÉGLAGES</button>  
    </div>  
  
    <div class="ws-banner" onclick="toggleTdDrawer()">  
      <div class="ws-left">  
        <span class="dot dot-grey"></span>  
        <div>  
          <div class="ws-text-main" id="ws-status-text">Wall Street fermée · ouvre lundi à 15 h 30</div>  
          <div class="ws-text-sub mono-text" id="ws-sub-text">Or 4 070,23 $ · 11 instruments réinitialisés à zéro</div>  
        </div>  
      </div>  
      <div style="color:var(--text-muted);">›</div>  
    </div>  
  
    <!-- Twelve Data Drawer -->  
    <div class="td-drawer" id="td-drawer">  
      <table class="td-table">  
        <thead>  
          <tr><th>Valeur</th><th>Cours · Source</th><th>Statut</th></tr>  
        </thead>  
        <tbody id="td-quotes-body"></tbody>  
      </table>  
      <div style="margin-top:10px;">  
        <label style="font-size:11.5px; color:var(--text-muted);">Clé API Twelve Data (optionnelle) :</label>  
        <input type="password" id="td-api-key" class="input-field" placeholder="Coller votre clé..." onchange="localStorage.setItem('HELIOS_TD_KEY', this.value.trim())" />  
      </div>  
      <button class="btn-block emerald" onclick="refreshQuotes()">LIRE LES COURS MAINTENANT</button>  
    </div>  
  </header>  
  
  <!-- CONTAINER -->  
  <main class="container">  
  
    <!-- ÉCRAN 0 : VUE D'ENSEMBLE -->  
    <section class="screen active" id="screen-accueil">  
      <div class="eyebrow">DÉPART À ZÉRO · AUCUNE POSITION ENGAGÉE</div>  
      <h1 class="page-title">VUE D'ENSEMBLE</h1>  
      <span class="broker-badge cyan">ProRealTime · Virtuel (Feuille propre)</span>  
  
      <div class="card">  
        <div class="section-label" style="margin-top:0;">1 · CAPITAL & DISPONIBILITÉS</div>  
        <div class="grid-2" style="margin-top:8px;">  
          <div>  
            <div style="font-size:12px; color:var(--text-muted);">Capital de départ</div>  
            <div class="mono-text" style="font-size:20px; font-weight:700;">10 000 $US</div>  
          </div>  
          <div>  
            <div style="font-size:12px; color:var(--text-muted);">Capital engagé</div>  
            <div class="mono-text" style="font-size:20px; font-weight:700; color:var(--emerald);">0 $ (0 %)</div>  
          </div>  
        </div>  
        <p class="mono-text" style="font-size:12.5px; color:var(--text-muted); margin-top:10px;">  
          Toutes les opérations perturbées ont été purgées. 11 ordres types sont disponibles dans l'onglet Ordres pour préparer votre nouvelle séance.  
        </p>  
      </div>  
  
      <div class="card">  
        <div class="section-label" style="margin-top:0;">2 · ORDRES À TRAITER</div>  
        <p style="font-size:13.5px; margin-bottom:10px;">  
          <strong id="acc-gen-count">11</strong> ordres prêts à être générés ou supprimés selon votre plan.  
        </p>  
        <button class="btn-block" onclick="switchScreen('ordres')">OUVRIR LA STATION DES ORDRES ›</button>  
      </div>  
    </section>  
  
    <!-- ÉCRAN 1 : VEILLE -->  
    <section class="screen" id="screen-veille">  
      <div class="eyebrow">SURVEILLANCE & SYNTHÈSES</div>  
      <h1 class="page-title">VEILLE</h1>  
      <div class="card">  
        <div style="display:flex; justify-content:space-between; align-items:center;">  
          <div style="display:flex; align-items:center; gap:8px;">  
            <span class="dot dot-green"></span>  
            <span style="font-size:13.5px; font-weight:600;">Veille synchronisée au 7 novembre 2026</span>  
          </div>  
          <button class="pill-top-btn" onclick="alert('Veille réactualisée')">Relancer</button>  
        </div>  
      </div>  
  
      <div class="section-label">CALENDRIER À VENIR · 7 PROCHAINS JOURS</div>  
      <div class="card" id="cal-container"></div>  
  
      <div class="section-label">SYNTHÈSES FONDAMENTALES (14)</div>  
      <div id="syntheses-container"></div>  
    </section>  
  
    <!-- ÉCRAN 2 : ORDRES -->  
    <section class="screen" id="screen-ordres">  
      <div class="eyebrow">TRAJECTOIRE · STATION AMONT</div>  
      <h1 class="page-title">ORDRES</h1>  
      <span class="broker-badge">Départ à zéro · Prêts à être arbitrés</span>  
  
      <div class="counter-grid">  
        <div class="counter-box" style="border-color:var(--border-emerald);">  
          <div class="counter-label">À GÉNÉRER / SAISIR</div>  
          <div class="counter-num" id="cnt-generes">11</div>  
        </div>  
        <div class="counter-box">  
          <div class="counter-label">EN ATTENTE COURTIER</div>  
          <div class="counter-num" id="cnt-attente">0</div>  
        </div>  
        <div class="counter-box">  
          <div class="counter-label">EN POSITION</div>  
          <div class="counter-num" id="cnt-position">0</div>  
        </div>  
      </div>  
  
      <div style="display:flex; justify-content:space-between; align-items:center; margin:16px 0 10px;">  
        <span class="section-label" style="margin:0;">ORDRES FIGÉS AU DÉPART (11)</span>  
        <button class="pill-top-btn" style="color:#ff9f9f; border-color:var(--border-alert);" onclick="deleteAllOrders()">TOUT SUPPRIMER</button>  
      </div>  
  
      <div id="ordres-list-container"></div>  
    </section>  
  
    <!-- ÉCRAN 3 : PORTEFEUILLE -->  
    <section class="screen" id="screen-exposition">  
      <div class="eyebrow">EXPOSITION & POSITIONS</div>  
      <h1 class="page-title">PORTEFEUILLE</h1>  
      <span class="broker-badge">Compte vierge</span>  
      <div class="card" style="text-align:center; padding:30px 16px;">  
        <div style="font-size:14px; color:var(--text-muted); margin-bottom:8px;">Aucune position ouverte actuellement.</div>  
        <div class="mono-text" style="font-size:24px; font-weight:700; color:var(--emerald);">10 000,00 $US DISPONIBLES</div>  
        <p style="font-size:12.5px; color:var(--text-dim); margin-top:10px;">  
          Lorsque vous déciderez de passer un ordre dans ProRealTime et de le marquer « En position », il viendra s'inscrire ici.  
        </p>  
      </div>  
    </section>  
  
    <!-- ÉCRAN 4 : JOURNAL / CONTRÔLE -->  
    <section class="screen" id="screen-journal">  
      <div class="eyebrow">JOURNAL SYSTÈME</div>  
      <h1 class="page-title">JOURNAL</h1>  
      <div class="card">  
        <div style="font-weight:700; font-size:15px; margin-bottom:4px;">Réinitialisation intégrale « Départ Jour 1 »</div>  
        <div class="mono-text" style="font-size:12px; color:var(--text-muted); margin-bottom:8px;">7 novembre 2026 · 05 h 15 CET</div>  
        <p style="font-size:13px; color:var(--text-muted);">  
          Toutes les opérations antérieures perturbées ont été effacées. Les 11 ordres modèles sont figés dans l'état « À générer / arbitrer ». Le capital papier est remis à 10 000 $US.  
        </p>  
      </div>  
    </section>  
  
    <!-- ÉCRAN 5 : RÉGLAGES & BASE DOCUMENTS.JSON -->  
    <section class="screen" id="screen-reglages">  
      <div class="eyebrow">PARAMÈTRES & DONNÉES</div>  
      <h1 class="page-title">RÉGLAGES</h1>  
      <div class="card">  
        <div class="section-label" style="margin-top:0;">BASE DOCUMENTS.JSON</div>  
        <p style="font-size:13px; color:var(--text-muted); margin-bottom:12px;">  
          Sauvegardez l'état de votre application dans un fichier JSON local à tout moment.  
        </p>  
        <div class="grid-2">  
          <button class="btn-block emerald" onclick="exportState()">EXPORTER JSON</button>  
          <button class="btn-block danger" onclick="resetToDayZero()">REMETTRE À ZÉRO</button>  
        </div>  
      </div>  
    </section>  
  
  </main>  
  
  <nav class="bottom-nav">  
    <div class="nav-tab active" id="tab-accueil" onclick="switchScreen('accueil')">Vue<br>d'ensemble</div>  
    <div class="nav-tab" id="tab-veille" onclick="switchScreen('veille')">Veille</div>  
    <div class="nav-tab" id="tab-ordres" onclick="switchScreen('ordres')">Ordres</div>  
    <div class="nav-tab" id="tab-exposition" onclick="switchScreen('exposition')">Portefeuille</div>  
  </nav>  
  
  <script>  
    // 11 Ordres types extraits de vos documents.json, réinitialisés comme s'ils venaient d'être proposés  
    const INITIAL_ORDERS = [  
      { id: "O-AMD",  sym: "AMD",     sens: "Achat",              qty: 1,  in: 463.21,  stop: 430.00, motif: "Repli zone Meta / test après résultats T3" },  
      { id: "O-CRWD", sym: "CRWD",    sens: "Achat",              qty: 1,  in: 216.92,  stop: 201.50, motif: "Zone demande 215–225 $ post Fortinet" },  
      { id: "O-DDOG", sym: "DDOG",    sens: "Achat",              qty: 3,  in: 280.70,  stop: 262.23, motif: "Rebond support logiciels / résultats T3" },  
      { id: "O-MRVL", sym: "MRVL",    sens: "Achat",              qty: 3,  in: 226.52,  stop: 210.04, motif: "Profil volume semi-conducteurs" },  
      { id: "O-MU",   sym: "MU",      sens: "Achat",              qty: 5,  in: 902.60,  stop: 864.55, motif: "Nœud de volume mémoire IA" },  
      { id: "O-NTAP", sym: "NTAP",    sens: "Achat",              qty: 5,  in: 164.66,  stop: 153.20, motif: "Support historique 160–165 $" },  
      { id: "O-PANW", sym: "PANW",    sens: "Achat",              qty: 2,  in: 334.75,  stop: 310.00, motif: "Zone de demande cybersécurité" },  
      { id: "O-VEEV", sym: "VEEV",    sens: "Achat",              qty: 14, in: 301.50,  stop: 288.99, motif: "Demande logicielle santé" },  
      { id: "O-VLO",  sym: "VLO",     sens: "Vente à découvert",  qty: 11, in: 416.56,  stop: 445.54, motif: "Offre diesel russe / marges raffinage" },  
      { id: "O-MPC",  sym: "MPC",     sens: "Vente à découvert",  qty: 10, in: 454.19,  stop: 487.56, motif: "Zone d'offre raffinage US" },  
      { id: "O-XAU",  sym: "XAU/USD", sens: "Achat",              qty: 1,  in: 3989.24, stop: 3961.06, motif: "Support or au comptant sous 4 000 $" }  
    ];  
  
    const CALENDRIER = [  
      { date: "lun. 9 nov.", titre: "Arrivée prévue du pétrolier Talisman (diesel russe) sur la côte Est US" },  
      { date: "mar. 10 nov. · 14 h 30", titre: "États-Unis : inflation CPI (octobre) — Impact direct taux & or" },  
      { date: "ven. 13 nov. · 14 h 30", titre: "États-Unis : prix à la production PPI (octobre)" },  
      { date: "mer. 18 nov. · 20 h 00", titre: "Fed : compte rendu officiel de la réunion du FOMC" },  
      { date: "mer. 18 nov. · 22 h 00", titre: "Palo Alto Networks (PANW) : résultats trimestriels" },  
      { date: "mer. 9 déc. · 20 h 00", titre: "Fed : décision sur les taux et nouvelles projections économiques" }  
    ];  
  
    const SYNTHESES = [  
      { date: "30 oct. 2026", titre: "Fed : deux responsables pour une hausse de taux", resume: "Déclarations bellicistes créant une onde de choc sur les technologiques et l'or fin octobre." },  
      { date: "30 oct. 2026", titre: "Ormuz & Houthis : tensions maritimes", resume: "Le brut reste soutenu au-dessus de 115 $, maintenant les incertitudes sur les raffineurs." },  
      { date: "29 oct. 2026", titre: "Marvell / Lumentum : spéculation de rachat", resume: "Craintes de dilution ayant provoqué de fortes variations sur le secteur des semi-conducteurs." },  
      { date: "29 oct. 2026", titre: "Résultats Big Tech & Cybersécurité", resume: "Choc Fortinet et révisions des flux de trésorerie sur les investissements IA." }  
    ];  
  
    const QUOTES = {  
      "AMD": 447.98, "CRWD": 216.92, "DDOG": 179.07, "MRVL": 141.08,  
      "MU": 884.74, "NTAP": 169.15, "PANW": 313.69, "VEEV": 312.96,  
      "VLO": 399.66, "MPC": 432.51, "XAU/USD": 4070.23  
    };  
  
    let orders = JSON.parse(localStorage.getItem("HELIOS_ZERO_ORDERS")) || INITIAL_ORDERS;  
  
    function render() {  
      // Compteurs  
      document.getElementById("cnt-generes").textContent = orders.length;  
      document.getElementById("acc-gen-count").textContent = orders.length;  
  
      // Table quotes Twelve Data  
      const tdBody = document.getElementById("td-quotes-body");  
      tdBody.innerHTML = Object.entries(QUOTES).map(([sym, p]) => `  
        <tr>  
          <td class="mono-text" style="font-weight:600;">${sym}</td>  
          <td class="mono-text">${p.toFixed(2)} $ · Twelve Data</td>  
          <td style="color:var(--text-muted); font-size:11px;">Clôture 6/7 nov.</td>  
        </tr>  
      `).join("");  
  
      // Liste des ordres  
      const cont = document.getElementById("ordres-list-container");  
      if (orders.length === 0) {  
        cont.innerHTML = `<div class="card" style="text-align:center; color:var(--text-muted);">Tous les ordres ont été supprimés. Feuille 100 % vierge.</div>`;  
      } else {  
        cont.innerHTML = orders.map((o, idx) => `  
          <div class="card">  
            <div class="card-header-row">  
              <div>  
                <span class="mono-text" style="font-size:18px; font-weight:700; margin-right:8px;">${o.sym}</span>  
                <span class="tag ${o.sens.includes('Vente') ? 'tag-sell' : 'tag-buy'}">${o.sens} ${o.qty}</span>  
              </div>  
              <span class="mono-text" style="color:var(--text-muted); font-size:13px;">Réf : ${o.stop.toFixed(2)} $</span>  
            </div>  
            <p class="mono-text" style="font-size:13.5px; margin:6px 0;">  
              Limite proposée : <strong>${o.in.toFixed(2)} $</strong> (Cours actuel : ${QUOTES[o.sym] ? QUOTES[o.sym].toFixed(2) + ' $' : '-'})  
            </p>  
            <p style="font-size:12.5px; color:var(--text-muted);">${o.motif}</p>  
            <div class="grid-2" style="margin-top:10px;">  
              <button class="btn-block" style="margin-top:0;" onclick="duplicateOrder(${idx})">+ DUPLIQUER</button>  
              <button class="btn-block danger" style="margin-top:0;" onclick="deleteOrder(${idx})">✕ SUPPRIMER</button>  
            </div>  
          </div>  
        `).join("");  
      }  
  
      // Calendrier & Synthèses  
      document.getElementById("cal-container").innerHTML = CALENDRIER.map(c => `  
        <div style="padding:8px 0; border-bottom:1px solid rgba(255,255,255,0.06);">  
          <div class="mono-text" style="font-size:12px; color:var(--emerald);">${c.date}</div>  
          <div style="font-size:13.5px; font-weight:600;">${c.titre}</div>  
        </div>  
      `).join("");  
  
      document.getElementById("syntheses-container").innerHTML = SYNTHESES.map(s => `  
        <div class="card">  
          <div style="font-size:11.5px; color:var(--text-muted);">${s.date}</div>  
          <div style="font-weight:700; font-size:14.5px; margin:3px 0;">${s.titre}</div>  
          <p style="font-size:13px; color:var(--text-muted);">${s.resume}</p>  
        </div>  
      `).join("");  
  
      localStorage.setItem("HELIOS_ZERO_ORDERS", JSON.stringify(orders));  
    }  
  
    function switchScreen(id) {  
      document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));  
      document.getElementById("screen-" + id).classList.add("active");  
      document.querySelectorAll(".nav-tab").forEach(t => t.classList.remove("active"));  
      const t = document.getElementById("tab-" + id);  
      if (t) t.classList.add("active");  
      window.scrollTo({ top: 0, behavior: "smooth" });  
    }  
  
    function toggleTdDrawer() {  
      document.getElementById("td-drawer").classList.toggle("open");  
    }  
  
    function deleteOrder(idx) {  
      orders.splice(idx, 1);  
      render();  
    }  
  
    function duplicateOrder(idx) {  
      const copy = { ...orders[idx], id: "O-" + Date.now() };  
      orders.splice(idx + 1, 0, copy);  
      render();  
    }  
  
    function deleteAllOrders() {  
      if (confirm("Supprimer tous les ordres modèles pour laisser la station 100 % vide ?")) {  
        orders = [];  
        render();  
      }  
    }  
  
    function resetToDayZero() {  
      if (confirm("Réinitialiser les 11 ordres types au jour 1 ?")) {  
        orders = [...INITIAL_ORDERS];  
        render();  
      }  
    }  
  
    function exportState() {  
      const data = {  
        meta: "Helios v7.2 Départ Jour 1",  
        date: new Date().toISOString(),  
        capital_usd: 10000,  
        orders: orders,  
        quotes: QUOTES  
      };  
      const blob = new Blob([JSON.stringify(data, null, 2)], { type: "application/json" });  
      const a = document.createElement("a");  
      a.href = URL.createObjectURL(blob);  
      a.download = `helios-reset-jour1-${new Date().toISOString().slice(0,10)}.json`;  
      a.click();  
    }  
  
    function refreshQuotes() {  
      alert("Cours Twelve Data déjà calés sur les clôtures officielles du week-end.");  
    }  
  
    render();  
  </script>  
</body>  
</html>  
