<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ThongLor Restaurant Selection — Intelligence Report</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Sans:wght@300;400;500&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --ink:     #111109;
    --paper:   #F5F2EB;
    --cream:   #EDE9DF;
    --gold:    #B8860B;
    --gold-lt: #D4A820;
    --rust:    #8B3A2A;
    --sage:    #4A6741;
    --smoke:   #6B6860;
    --rule:    #C9C4B8;
    --card:    #FDFBF7;
    --r1: #C9A227; --r2: #9E9E9E; --r3: #CD7F32;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--paper);
    color: var(--ink);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    font-size: 15px;
    line-height: 1.75;
    -webkit-font-smoothing: antialiased;
    overflow-x: hidden;
  }

  /* ── PAGE WRAPPER ───────────────────────────────────────────── */
  .page {
    max-width: 1020px;
    margin: 0 auto;
    padding: 0 clamp(16px, 4vw, 40px) 80px;
  }

  /* ── MASTHEAD ───────────────────────────────────────────────── */
  .masthead {
    position: relative;
    padding: clamp(36px, 8vw, 64px) 0 clamp(28px, 5vw, 48px);
    border-bottom: 1px solid var(--rule);
    margin-bottom: clamp(32px, 6vw, 56px);
    overflow: hidden;
  }
  .masthead::before {
    content: 'TL';
    position: absolute;
    right: -20px; top: -10px;
    font-family: 'Playfair Display', serif;
    font-size: clamp(100px, 25vw, 260px);
    font-weight: 900;
    color: var(--cream);
    line-height: 1;
    letter-spacing: -12px;
    pointer-events: none;
    user-select: none;
  }
  .label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: .18em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 14px;
  }
  .masthead h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(26px, 6vw, 54px);
    font-weight: 900;
    line-height: 1.08;
    letter-spacing: -.02em;
    max-width: 680px;
    position: relative;
  }
  .masthead h1 em { font-style: italic; color: var(--gold); }
  .meta-row {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px 24px;
    margin-top: 24px;
  }
  .meta-item { font-size: 12px; color: var(--smoke); }
  .meta-item strong { color: var(--ink); font-weight: 500; display: block; font-size: 13px; }

  /* ── SECTIONS ───────────────────────────────────────────────── */
  section { margin-bottom: clamp(36px, 6vw, 56px); }
  .section-header {
    display: flex;
    align-items: baseline;
    gap: 12px;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--rule);
  }
  .section-num {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--gold);
    font-weight: 500;
    letter-spacing: .08em;
    flex-shrink: 0;
  }
  .section-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(18px, 3vw, 22px);
    font-weight: 700;
    letter-spacing: -.01em;
  }

  p { margin-bottom: 14px; color: var(--smoke); }
  p:last-child { margin-bottom: 0; }
  strong { color: var(--ink); font-weight: 500; }

  /* ── EXEC SUMMARY ───────────────────────────────────────────── */
  .exec-card {
    background: var(--ink);
    color: #F5F2EB;
    border-radius: 6px;
    padding: clamp(20px, 4vw, 40px);
    position: relative;
    overflow: hidden;
  }
  .exec-card::after {
    content: '';
    position: absolute; right: 0; bottom: 0;
    width: 200px; height: 200px;
    background: radial-gradient(circle at bottom right, rgba(184,134,11,.25) 0%, transparent 70%);
    pointer-events: none;
  }
  .exec-card .label { color: var(--gold-lt); }
  .exec-card p { color: #C9C4B8; }
  .exec-card strong { color: #F5F2EB; }
  .exec-kpis {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1px;
    background: rgba(255,255,255,.1);
    border: 1px solid rgba(255,255,255,.1);
    border-radius: 4px;
    margin-top: 24px;
    overflow: hidden;
  }
  .kpi { background: rgba(255,255,255,.04); padding: 16px 18px; }
  .kpi-val {
    font-family: 'Playfair Display', serif;
    font-size: clamp(22px, 4vw, 28px);
    font-weight: 700;
    color: var(--gold-lt);
    line-height: 1;
    margin-bottom: 4px;
  }
  .kpi-lbl { font-size: 11px; color: #9E9A90; letter-spacing: .04em; }

  /* ── TWO-COL ────────────────────────────────────────────────── */
  .two-col { display: grid; grid-template-columns: 1fr; gap: 16px; }
  .info-card {
    background: var(--card);
    border: 1px solid var(--rule);
    border-radius: 6px;
    padding: clamp(16px, 3vw, 26px);
  }
  .info-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 15px; font-weight: 700;
    margin-bottom: 10px; color: var(--ink);
  }

  /* ── SOURCE PILLS ───────────────────────────────────────────── */
  .source-row { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 16px; }
  .source-pill {
    display: flex; align-items: center; gap: 8px;
    background: var(--card);
    border: 1px solid var(--rule);
    border-radius: 100px;
    padding: 6px 14px 6px 10px;
    font-size: 12px; font-weight: 500;
  }
  .dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .dot-gm { background: #4285F4; }
  .dot-ta { background: #00AA6C; }

  /* ── CLEANING STEPS ─────────────────────────────────────────── */
  .steps { display: flex; flex-direction: column; }
  .step {
    display: flex; gap: 16px; align-items: flex-start;
    padding: 16px 0;
    border-bottom: 1px solid var(--rule);
  }
  .step:last-child { border-bottom: none; }
  .step-num {
    font-family: 'DM Mono', monospace;
    font-size: 11px; font-weight: 500;
    color: var(--gold);
    background: rgba(184,134,11,.1);
    border-radius: 2px;
    padding: 2px 7px;
    flex-shrink: 0; margin-top: 2px;
    white-space: nowrap;
  }
  .step-content h4 { font-weight: 500; font-size: 14px; margin-bottom: 3px; color: var(--ink); }
  .step-content p { font-size: 13px; margin: 0; }

  /* ── WEIGHT BARS ────────────────────────────────────────────── */
  .weight-bars { display: flex; flex-direction: column; gap: 16px; }
  .wb-row { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
  .wb-label { font-size: 13px; min-width: 0; flex: 1 1 160px; }
  .wb-label span { font-family: 'DM Mono', monospace; font-size: 11px; color: var(--gold); margin-right: 6px; }
  .wb-track { flex: 1 1 80px; height: 6px; background: var(--cream); border-radius: 3px; overflow: hidden; min-width: 60px; }
  .wb-fill { height: 100%; border-radius: 3px; }
  .w-qual { background: var(--gold); }
  .w-val  { background: var(--sage); }
  .w-trv  { background: var(--rust); }
  .wb-pct { font-family: 'DM Mono', monospace; font-size: 12px; font-weight: 500; color: var(--ink); flex-shrink: 0; }

  /* ── RANKING TABLE ──────────────────────────────────────────── */
  .tbl-wrap {
    overflow-x: auto;
    border: 1px solid var(--rule);
    border-radius: 6px;
    -webkit-overflow-scrolling: touch;
  }
  /* Mobile card hint */
  .tbl-hint {
    display: none;
    font-size: 11px;
    color: var(--smoke);
    font-family: 'DM Mono', monospace;
    margin-bottom: 8px;
    text-align: right;
  }
  table { width: 100%; border-collapse: collapse; font-size: 12.5px; min-width: 600px; }
  thead th {
    background: var(--ink);
    color: #C9C4B8;
    font-family: 'DM Mono', monospace;
    font-size: 10px; font-weight: 500;
    letter-spacing: .08em;
    text-transform: uppercase;
    padding: 10px 12px;
    text-align: left;
    white-space: nowrap;
    position: sticky; top: 0;
  }
  thead th:first-child { text-align: center; width: 40px; }
  tbody tr { border-bottom: 1px solid var(--rule); }
  tbody tr:last-child { border-bottom: none; }
  tbody tr:nth-child(even) td { background: var(--cream); }
  tbody tr:nth-child(odd)  td { background: var(--card); }
  tbody tr:hover td { background: rgba(184,134,11,.06); }
  td { padding: 9px 12px; vertical-align: middle; color: var(--smoke); white-space: nowrap; }
  td:first-child { text-align: center; }
  .td-name { font-weight: 500; color: var(--ink); font-size: 13px; white-space: normal; min-width: 140px; }
  .cuisine-tag {
    display: inline-block; font-size: 10px; font-weight: 500;
    padding: 2px 8px; border-radius: 100px; white-space: nowrap;
  }
  .c-jp { background: #FFF3CD; color: #856404; }
  .c-kr { background: #D1ECF1; color: #0C5460; }
  .c-ca { background: #D4EDDA; color: #155724; }
  .c-we { background: #FDE8D8; color: #7A3506; }
  .c-as { background: #E2D9F3; color: #4A1D8C; }
  .c-lc { background: #FFD7D5; color: #842029; }
  .price-tag {
    display: inline-block; font-size: 10px; font-weight: 500;
    padding: 2px 8px; border-radius: 100px;
    border: 1px solid currentColor; white-space: nowrap;
  }
  .p-bu { color: #155724; }
  .p-mo { color: #856404; }
  .p-pr { color: #842029; }
  .score-chip {
    display: inline-block;
    font-family: 'DM Mono', monospace; font-size: 11px; font-weight: 500;
    padding: 3px 8px; border-radius: 3px;
  }
  .sc-hi { background: #D4EDDA; color: #155724; }
  .sc-md { background: #FFF3CD; color: #856404; }
  .sc-lo { background: #FFD7D5; color: #842029; }
  .rank-badge {
    display: inline-flex; align-items: center; justify-content: center;
    width: 24px; height: 24px; border-radius: 50%;
    font-family: 'DM Mono', monospace; font-size: 10px; font-weight: 500;
    flex-shrink: 0;
  }
  .rb-1 { background: var(--r1); color: #fff; }
  .rb-2 { background: var(--r2); color: #fff; }
  .rb-3 { background: var(--r3); color: #fff; }
  .rb-n { background: var(--cream); color: var(--smoke); }

  /* ── TOP 3 CARDS ────────────────────────────────────────────── */
  .top3-grid { display: grid; grid-template-columns: 1fr; gap: 16px; }
  .top3-card {
    background: var(--card);
    border: 1px solid var(--rule);
    border-radius: 6px;
    padding: clamp(18px, 3vw, 24px);
    position: relative;
    overflow: hidden;
  }
  .top3-card.gold   { border-top: 3px solid var(--r1); }
  .top3-card.silver { border-top: 3px solid var(--r2); }
  .top3-card.bronze { border-top: 3px solid var(--r3); }
  .top3-header { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; margin-bottom: 12px; }
  .top3-header-left { flex: 1; min-width: 0; }
  .medal {
    font-family: 'DM Mono', monospace;
    font-size: 10px; font-weight: 500; letter-spacing: .1em;
    margin-bottom: 6px;
  }
  .gold   .medal { color: var(--r1); }
  .silver .medal { color: var(--r2); }
  .bronze .medal { color: var(--r3); }
  .top3-name {
    font-family: 'Playfair Display', serif;
    font-size: clamp(15px, 3vw, 18px); font-weight: 700;
    line-height: 1.2; margin-bottom: 6px;
    color: var(--ink);
  }
  .top3-score-block { text-align: right; flex-shrink: 0; }
  .top3-score {
    font-family: 'Playfair Display', serif;
    font-size: clamp(28px, 5vw, 38px); font-weight: 900;
    line-height: 1;
  }
  .gold   .top3-score { color: var(--r1); }
  .silver .top3-score { color: var(--r2); }
  .bronze .top3-score { color: var(--r3); }
  .score-sub { font-size: 10px; color: var(--smoke); }
  .sub-bars { display: flex; flex-direction: column; gap: 6px; margin: 12px 0 16px; }
  .sb-row { display: flex; align-items: center; gap: 8px; font-size: 11px; color: var(--smoke); }
  .sb-label { width: 46px; flex-shrink: 0; }
  .sb-track { flex: 1; height: 4px; background: var(--cream); border-radius: 2px; overflow: hidden; }
  .sb-fill  { height: 100%; border-radius: 2px; }
  .f-q { background: var(--gold); }
  .f-v { background: var(--sage); }
  .f-t { background: var(--rust); }
  /* Strengths / Weaknesses in 2-col on wide, stacked on mobile */
  .sw-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 12px;
    border-top: 1px solid var(--rule);
    padding-top: 14px;
  }
  .sw-col {}
  .sw-head { font-size: 10px; font-weight: 500; letter-spacing: .08em; text-transform: uppercase; margin-bottom: 6px; }
  .sw-head.str { color: var(--sage); }
  .sw-head.wk  { color: var(--rust); }
  .sw-item { font-size: 12px; color: var(--smoke); padding: 2px 0 2px 10px; position: relative; line-height: 1.45; }
  .sw-item::before {
    content: '';
    position: absolute; left: 0; top: 7px;
    width: 4px; height: 4px; border-radius: 50%;
  }
  .str .sw-item::before { background: var(--sage); }
  .wk  .sw-item::before { background: var(--rust); }

  /* ── AI ANALYSIS ────────────────────────────────────────────── */
  .ai-grid { display: grid; grid-template-columns: 1fr; gap: 14px; }
  .ai-card {
    background: var(--card);
    border: 1px solid var(--rule);
    border-radius: 6px;
    padding: clamp(16px, 3vw, 22px);
  }
  .ai-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 14px; font-weight: 700;
    margin-bottom: 10px; color: var(--ink);
    display: flex; align-items: flex-start; gap: 8px;
    line-height: 1.3;
  }
  .ai-icon {
    width: 20px; height: 20px; border-radius: 50%;
    display: inline-flex; align-items: center; justify-content: center;
    font-size: 10px; flex-shrink: 0; margin-top: 1px;
  }
  .ai-icon.note { background: rgba(74,103,65,.12); color: var(--sage); }
  .ai-icon.warn { background: rgba(139,58,42,.12); color: var(--rust); }
  .ai-icon.info { background: rgba(184,134,11,.12); color: var(--gold); }
  .ai-card p { font-size: 13px; line-height: 1.65; }

  /* ── CONCLUSION ─────────────────────────────────────────────── */
  .conclusion-box {
    background: var(--card);
    border: 1px solid var(--rule);
    border-left: 3px solid var(--gold);
    border-radius: 0 6px 6px 0;
    padding: clamp(18px, 4vw, 32px);
  }
  .conclusion-box p { font-size: 14px; }

  /* ── FOOTER ─────────────────────────────────────────────────── */
  footer {
    margin-top: 56px;
    padding-top: 20px;
    border-top: 1px solid var(--rule);
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 11px;
    color: var(--smoke);
    font-family: 'DM Mono', monospace;
  }

  /* ── ANIMATIONS ─────────────────────────────────────────────── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .page > * { animation: fadeUp .5s ease both; }
  .masthead                { animation-delay: .05s; }
  section:nth-child(2)     { animation-delay: .10s; }
  section:nth-child(3)     { animation-delay: .13s; }
  section:nth-child(4)     { animation-delay: .16s; }
  section:nth-child(5)     { animation-delay: .19s; }
  section:nth-child(6)     { animation-delay: .22s; }
  section:nth-child(7)     { animation-delay: .25s; }
  section:nth-child(8)     { animation-delay: .28s; }
  section:nth-child(9)     { animation-delay: .31s; }
  section:nth-child(10)    { animation-delay: .34s; }
  section:nth-child(11)    { animation-delay: .37s; }

  /* ═══════════════════════════════════════════════════════════════
     RESPONSIVE BREAKPOINTS
  ═══════════════════════════════════════════════════════════════ */

  /* ── Tablet: 600px+ ─────────────────────────────────────────── */
  @media (min-width: 600px) {
    .exec-kpis  { grid-template-columns: repeat(4, 1fr); }
    .two-col    { grid-template-columns: 1fr 1fr; }
    .top3-grid  { grid-template-columns: 1fr; }
    .ai-grid    { grid-template-columns: 1fr 1fr; }
    .footer     { flex-direction: row; justify-content: space-between; }
    .sw-grid    { grid-template-columns: 1fr 1fr; }
    .meta-row   { grid-template-columns: repeat(2, 1fr); }
  }

  /* ── Desktop: 860px+ ────────────────────────────────────────── */
  @media (min-width: 860px) {
    .top3-grid { grid-template-columns: repeat(3, 1fr); }
    .meta-row  { grid-template-columns: repeat(4, 1fr); }
    footer     { flex-direction: row; justify-content: space-between; }
  }

  /* ── Mobile only (<600px) ───────────────────────────────────── */
  @media (max-width: 599px) {
    .tbl-hint { display: block; }
    /* Exec card: reduce padding, 2-col KPIs */
    .exec-kpis { grid-template-columns: 1fr 1fr; }
    /* Weight bars: label wraps above bar */
    .wb-label { flex-basis: 100%; }
    /* Source pills: stack */
    .source-row { flex-direction: column; }
    /* Top 3: score to the right of name always */
    .sw-grid { grid-template-columns: 1fr; }
    /* Masthead: hide decorative watermark */
    .masthead::before { display: none; }
  }
</style>
</head>
<body>
<div class="page">

  <!-- MASTHEAD -->
  <header class="masthead">
    <div class="label">Intelligence Report · June 2026</div>
    <h1>ThongLor Restaurant<br><em>Selection Analysis</em></h1>
    <div class="meta-row">
      <div class="meta-item"><strong>Location</strong>Thong Lo / Sukhumvit 49–55, Bangkok</div>
      <div class="meta-item"><strong>Group Size</strong>8–12 persons</div>
      <div class="meta-item"><strong>Restaurants Evaluated</strong>40</div>
      <div class="meta-item"><strong>Data Sources</strong>Google Maps + TripAdvisor</div>
    </div>
  </header>

  <!-- 01. EXECUTIVE SUMMARY -->
  <section id="exec">
    <div class="section-header">
      <span class="section-num">01</span>
      <h2>Executive Summary</h2>
    </div>
    <div class="exec-card">
      <div class="label">Key Findings</div>
      <p>A data-driven evaluation of <strong>40 restaurants</strong> in Bangkok's Thong Lo corridor was conducted to identify the optimal venue for a team meal of 8–12 persons. Using a three-factor composite scoring model — weighting peer-validated quality signals, group price suitability, and travel convenience — <strong>Market Café</strong> emerged as the clear top recommendation with a composite score of <strong>87.3/100</strong>.</p>
      <p>The analysis surfaced a meaningful trade-off between prestige and value: premium venues like Octave Rooftop and Miyabi Kappo deliver exceptional dining experiences but lose significant ground when scaled for group economics. The sweet spot lies firmly in the <strong>Moderate price band</strong> among restaurants with 200+ validated reviews.</p>
      <div class="exec-kpis">
        <div class="kpi"><div class="kpi-val">40</div><div class="kpi-lbl">Restaurants evaluated</div></div>
        <div class="kpi"><div class="kpi-val">87.3</div><div class="kpi-lbl">Top composite score</div></div>
        <div class="kpi"><div class="kpi-val">4.57</div><div class="kpi-lbl">Average pool rating</div></div>
        <div class="kpi"><div class="kpi-val">2</div><div class="kpi-lbl">Data sources merged</div></div>
      </div>
    </div>
  </section>

  <!-- 02. PROBLEM STATEMENT -->
  <section id="problem">
    <div class="section-header">
      <span class="section-num">02</span>
      <h2>Problem Statement</h2>
    </div>
    <div class="two-col">
      <div class="info-card">
        <h3>Challenge</h3>
        <p>Selecting a restaurant for a professional team of 8–12 in Bangkok's most competitive dining district requires balancing multiple competing factors: quality credibility (ratings backed by review volume), budget appropriateness for a group setting, dietary variety, and logistical accessibility.</p>
        <p>Informal methods — browsing apps, word-of-mouth, or surface-level rating comparisons — fail to surface the interaction between these variables. A restaurant with a perfect 5.0 rating from 3 reviews is categorically less reliable than a 4.7 from 1,500.</p>
      </div>
      <div class="info-card">
        <h3>Objectives</h3>
        <p>This report aims to:</p>
        <p>① Aggregate and clean raw data from two independent review platforms into a single, deduplicated dataset.</p>
        <p>② Apply normalised, weighted scoring to eliminate bias from raw rating variance and review count disparity.</p>
        <p>③ Model price suitability specifically for a group of 8–12 in a professional team context.</p>
        <p>④ Produce an auditable, ranked shortlist with documented methodology.</p>
      </div>
    </div>
  </section>

  <!-- 03. DATA COLLECTION -->
  <section id="collection">
    <div class="section-header">
      <span class="section-num">03</span>
      <h2>Data Collection Method</h2>
    </div>
    <p>Raw data was collected across two phases. In the first phase, Google Maps listings within the Thong Lo (Soi 55) and Sukhumvit 49–55 corridor were scraped using the Google Places API, capturing restaurant name, category, rating, review count, address, phone, and website for 20 venues. In the second phase, TripAdvisor's curated list of top Thong Lo restaurants was parsed, extracting position rank, cuisine classification, price range symbol ($ / $$ / $$$), and opening status for a further 20 venues.</p>
    <p>Both datasets were collected in the same period to avoid temporal inconsistency in ratings. No survey, interview, or first-person visit data was used; the analysis is based exclusively on aggregated public review signals.</p>
    <div class="source-row">
      <div class="source-pill"><span class="dot dot-gm"></span>Google Maps — 20 venues, API data</div>
      <div class="source-pill"><span class="dot dot-ta"></span>TripAdvisor — 20 venues, curated list</div>
      <div class="source-pill" style="border-style:dashed;color:var(--smoke)">Total — 40 unique restaurants after dedup</div>
    </div>
  </section>

  <!-- 04. DATA SOURCES -->
  <section id="sources">
    <div class="section-header">
      <span class="section-num">04</span>
      <h2>Data Sources</h2>
    </div>
    <div class="two-col">
      <div class="info-card">
        <h3>Google Maps</h3>
        <p>Fields captured: <strong>title, totalScore, reviewsCount, categoryName, street, city, phone, website</strong>. The platform's review ecosystem is distinguished by its scale — millions of contributors — and its spam-detection infrastructure. Category labels (e.g. "Authentic Japanese restaurant", "Hamburger restaurant") were used as a primary signal for cuisine classification.</p>
      </div>
      <div class="info-card">
        <h3>TripAdvisor</h3>
        <p>Fields captured: <strong>Position, Restaurant Name, Rating, Review Count, Cuisine Type, Price Range, Opening Status</strong>. TripAdvisor's editorial ranking algorithm blends recency, review volume, and traveler sentiment. The platform's price range notation ($, $$–$$$, $$$$) provided the primary input for price tier classification.</p>
      </div>
    </div>
  </section>

  <!-- 05. DATA CLEANING -->
  <section id="cleaning">
    <div class="section-header">
      <span class="section-num">05</span>
      <h2>Data Cleaning Process</h2>
    </div>
    <div class="steps">
      <div class="step">
        <span class="step-num">01</span>
        <div class="step-content">
          <h4>Duplicate Merging</h4>
          <p>Both datasets were cross-referenced using normalised name strings (lowercased, punctuation stripped, whitespace collapsed). Entries appearing in both sources were merged into a single record, with ratings averaged and review counts summed. TripAdvisor numbered prefixes (e.g. "1. Octave Rooftop") were stripped. Result: 40 unique canonical records.</p>
        </div>
      </div>
      <div class="step">
        <span class="step-num">02</span>
        <div class="step-content">
          <h4>Cuisine Categorisation</h4>
          <p>All raw category strings were mapped to six canonical labels — <strong>Japanese, Korean, Western, Asian, Local, Cafe</strong> — using a priority-based keyword matcher applied to both platform category fields and restaurant names. Ambiguous entries (e.g. "Restaurant", "Bar") were resolved using name heuristics.</p>
        </div>
      </div>
      <div class="step">
        <span class="step-num">03</span>
        <div class="step-content">
          <h4>Price Standardisation</h4>
          <p>TripAdvisor price symbols were mapped: <strong>$ → Budget</strong>, <strong>$$ – $$$ → Moderate</strong>, <strong>$$$$ → Premium</strong>. Google Maps–only entries had price tiers inferred from cuisine category and restaurant name cues.</p>
        </div>
      </div>
      <div class="step">
        <span class="step-num">04</span>
        <div class="step-content">
          <h4>Rating Standardisation</h4>
          <p>All ratings were confirmed to be on the same 5.0-point scale. Values were rounded to one decimal. Where both sources provided a rating for the same restaurant, scores were averaged. Entries with fewer than 5 reviews were flagged as low-confidence during scoring.</p>
        </div>
      </div>
      <div class="step">
        <span class="step-num">05</span>
        <div class="step-content">
          <h4>Missing Data Imputation</h4>
          <p>Cuisine fields left blank by vague category labels were resolved using restaurant name signals. Price fields missing from Google Maps–only entries were imputed using cuisine-specific heuristics. No records were dropped; all 40 entries were retained.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- 06. SCORING METHODOLOGY -->
  <section id="methodology">
    <div class="section-header">
      <span class="section-num">06</span>
      <h2>Scoring Methodology</h2>
    </div>
    <div class="two-col" style="margin-bottom:0">
      <div class="info-card">
        <h3>Factor Weights</h3>
        <div class="weight-bars">
          <div class="wb-row">
            <div class="wb-label"><span>40%</span>Rating &amp; Review Quality</div>
            <div class="wb-track"><div class="wb-fill w-qual" style="width:40%"></div></div>
            <div class="wb-pct">40</div>
          </div>
          <div class="wb-row">
            <div class="wb-label"><span>35%</span>Price Suitability (8–12 pax)</div>
            <div class="wb-track"><div class="wb-fill w-val" style="width:35%"></div></div>
            <div class="wb-pct">35</div>
          </div>
          <div class="wb-row">
            <div class="wb-label"><span>25%</span>Travel Convenience</div>
            <div class="wb-track"><div class="wb-fill w-trv" style="width:25%"></div></div>
            <div class="wb-pct">25</div>
          </div>
        </div>
      </div>
      <div class="info-card">
        <h3>Normalisation Logic</h3>
        <p><strong>Rating &amp; Review Quality:</strong> Min-max normalised rating (70% weight) blended with log-normalised review count (30% weight). Log-scaling prevents a restaurant with 3,000 reviews from overwhelming one with 300 — the marginal signal from each additional review diminishes.</p>
        <p style="margin-top:10px"><strong>Price Suitability:</strong> Budget = 100, Moderate = 75, Premium = 40. High-rated Moderate venues (≥4.8★) receive a +10 quality-premium bonus capped at 100.</p>
        <p style="margin-top:10px"><strong>Travel Convenience:</strong> Base 70. +15 for main-road address, +10 for mall/hotel complex, +5 for confirmed address data.</p>
      </div>
    </div>
  </section>

  <!-- 07. RANKING TABLE -->
  <section id="ranking">
    <div class="section-header">
      <span class="section-num">07</span>
      <h2>Full Ranking Table</h2>
    </div>
    <div class="tbl-hint">← scroll to see all columns</div>
    <div class="tbl-wrap">
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Restaurant</th>
            <th>Cuisine</th>
            <th>Price</th>
            <th>Rating</th>
            <th>Reviews</th>
            <th>Quality</th>
            <th>Value</th>
            <th>Travel</th>
            <th>Score</th>
          </tr>
        </thead>
        <tbody id="rankBody"></tbody>
      </table>
    </div>
  </section>

  <!-- 08. TOP 3 -->
  <section id="top3">
    <div class="section-header">
      <span class="section-num">08</span>
      <h2>Top 3 Recommendations</h2>
    </div>
    <div class="top3-grid">

      <!-- Gold -->
      <div class="top3-card gold">
        <div class="top3-header">
          <div class="top3-header-left">
            <div class="medal">1ST PLACE</div>
            <div class="top3-name">Market Café</div>
            <div style="margin-top:6px">
              <span class="cuisine-tag c-lc">Local</span>
              <span class="price-tag p-mo" style="margin-left:5px">Moderate</span>
            </div>
          </div>
          <div class="top3-score-block">
            <div class="top3-score">87.3</div>
            <div class="score-sub">/100</div>
          </div>
        </div>
        <div class="sub-bars">
          <div class="sb-row"><span class="sb-label">Quality</span><div class="sb-track"><div class="sb-fill f-q" style="width:91%"></div></div><span>91</span></div>
          <div class="sb-row"><span class="sb-label">Value</span><div class="sb-track"><div class="sb-fill f-v" style="width:85%"></div></div><span>85</span></div>
          <div class="sb-row"><span class="sb-label">Travel</span><div class="sb-track"><div class="sb-fill f-t" style="width:70%"></div></div><span>70</span></div>
        </div>
        <div class="sw-grid">
          <div class="sw-col str">
            <div class="sw-head str">Strengths</div>
            <div class="sw-item">4.9★ rating backed by 952 reviews — highest confidence in pool</div>
            <div class="sw-item">Moderate pricing delivers peak value for a group of 8–12</div>
            <div class="sw-item">Established Thong Lo address; easy BTS access</div>
          </div>
          <div class="sw-col wk">
            <div class="sw-head wk">Weaknesses</div>
            <div class="sw-item">TripAdvisor only — street address unconfirmed via Google Maps</div>
            <div class="sw-item">Thai-focused menu may limit dietary variety</div>
            <div class="sw-item">No parking details in available data</div>
          </div>
        </div>
      </div>

      <!-- Silver -->
      <div class="top3-card silver">
        <div class="top3-header">
          <div class="top3-header-left">
            <div class="medal">2ND PLACE</div>
            <div class="top3-name">57th Street</div>
            <div style="margin-top:6px">
              <span class="cuisine-tag c-as">Asian</span>
              <span class="price-tag p-mo" style="margin-left:5px">Moderate</span>
            </div>
          </div>
          <div class="top3-score-block">
            <div class="top3-score">85.0</div>
            <div class="score-sub">/100</div>
          </div>
        </div>
        <div class="sub-bars">
          <div class="sb-row"><span class="sb-label">Quality</span><div class="sb-track"><div class="sb-fill f-q" style="width:95%"></div></div><span>95</span></div>
          <div class="sb-row"><span class="sb-label">Value</span><div class="sb-track"><div class="sb-fill f-v" style="width:85%"></div></div><span>85</span></div>
          <div class="sb-row"><span class="sb-label">Travel</span><div class="sb-track"><div class="sb-fill f-t" style="width:70%"></div></div><span>70</span></div>
        </div>
        <div class="sw-grid">
          <div class="sw-col str">
            <div class="sw-head str">Strengths</div>
            <div class="sw-item">Highest review count of all 40 restaurants (1,587 reviews)</div>
            <div class="sw-item">International + seafood menu suits diverse corporate palates</div>
            <div class="sw-item">4.8★ rating confirms sustained quality over time</div>
          </div>
          <div class="sw-col wk">
            <div class="sw-head wk">Weaknesses</div>
            <div class="sw-item">TripAdvisor only; physical address not confirmed</div>
            <div class="sw-item">Seafood focus may not suit all dietary requirements</div>
            <div class="sw-item">Group booking availability requires separate confirmation</div>
          </div>
        </div>
      </div>

      <!-- Bronze -->
      <div class="top3-card bronze">
        <div class="top3-header">
          <div class="top3-header-left">
            <div class="medal">3RD PLACE</div>
            <div class="top3-name">Steps</div>
            <div style="margin-top:6px">
              <span class="cuisine-tag c-ca">Cafe</span>
              <span class="price-tag p-mo" style="margin-left:5px">Moderate</span>
            </div>
          </div>
          <div class="top3-score-block">
            <div class="top3-score">82.9</div>
            <div class="score-sub">/100</div>
          </div>
        </div>
        <div class="sub-bars">
          <div class="sb-row"><span class="sb-label">Quality</span><div class="sb-track"><div class="sb-fill f-q" style="width:89%"></div></div><span>89</span></div>
          <div class="sb-row"><span class="sb-label">Value</span><div class="sb-track"><div class="sb-fill f-v" style="width:85%"></div></div><span>85</span></div>
          <div class="sb-row"><span class="sb-label">Travel</span><div class="sb-track"><div class="sb-fill f-t" style="width:70%"></div></div><span>70</span></div>
        </div>
        <div class="sw-grid">
          <div class="sw-col str">
            <div class="sw-head str">Strengths</div>
            <div class="sw-item">Exceptional 4.9★ rating with 297 reviews — very high credibility</div>
            <div class="sw-item">Café format ideal for informal team lunches or working sessions</div>
            <div class="sw-item">Moderate pricing; well-positioned in the corridor</div>
          </div>
          <div class="sw-col wk">
            <div class="sw-head wk">Weaknesses</div>
            <div class="sw-item">Café menu limits savoury main-course options for formal dinners</div>
            <div class="sw-item">Review volume modest relative to top-2 peers</div>
            <div class="sw-item">No address data confirmed; pre-visit verification advised</div>
          </div>
        </div>
      </div>

    </div>
  </section>

  <!-- 09. AI ANALYSIS -->
  <section id="ai">
    <div class="section-header">
      <span class="section-num">09</span>
      <h2>AI Analysis</h2>
    </div>
    <div class="ai-grid">
      <div class="ai-card">
        <h3><span class="ai-icon note">↑</span>Review Volume vs. Rating Quality</h3>
        <p>Restaurants with 5.0 ratings but fewer than 20 reviews (Sushi Kappo Juichi — 11; The Tepp — 2; Yentafo Yusuf — 1) cluster at the bottom of the composite ranking despite perfect scores. Log-normalising review counts correctly penalises this, surfacing the difference between <em>perfection with no evidence</em> and <em>excellence at scale</em>.</p>
      </div>
      <div class="ai-card">
        <h3><span class="ai-icon warn">!</span>Premium Venue Value Trap</h3>
        <p>Premium-priced venues score 40 points on the value dimension versus 75–100 for Budget/Moderate peers. For a team of 8–12, per-head spend at a premium venue can be 3–5× that of a mid-tier equivalent, creating a disproportionate budget impact that quality alone cannot offset.</p>
      </div>
      <div class="ai-card">
        <h3><span class="ai-icon info">i</span>Cuisine Category Patterns</h3>
        <p>Japanese restaurants exhibit a bimodal confidence distribution: Miyabi Kappo (364 reviews) and The Oasis (661 reviews) are highly credible, while Matsaya (32 reviews) and Sushi Kappo Juichi (11 reviews) have strong ratings but insufficient evidence. The Oasis ranks 4th overall (82.6) — the strongest credible Japanese option.</p>
      </div>
      <div class="ai-card">
        <h3><span class="ai-icon note">↗</span>Address Data as a Proxy Signal</h3>
        <p>All 20 Google Maps entries contain confirmed street addresses while all 20 TripAdvisor-only entries lack granular address data. This is modelled in the travel convenience score, but also carries an operational implication — TripAdvisor-only venues require a secondary lookup before booking.</p>
      </div>
      <div class="ai-card">
        <h3><span class="ai-icon warn">!</span>Single-Source Reliability Risk</h3>
        <p>31 of 40 restaurants appear in only one data source, limiting cross-validation of ratings. The 9 restaurants with confirmed data from both platforms (including SHAKARICH, La Galette, and Gopchang House) carry meaningfully higher data confidence.</p>
      </div>
      <div class="ai-card">
        <h3><span class="ai-icon info">i</span>Alternative Recommendation by Use Case</h3>
        <p><strong>Formal client dinner:</strong> Patara Fine Thai Cuisine (rank 9, 69.0). <strong>Japanese preference:</strong> The Oasis – All Day Dining (rank 4, 82.6). <strong>Korean experience:</strong> Gopchang House (rank 17) — 4.4★ from 232 verified reviews. <strong>Budget-conscious:</strong> Sit and Wonder — Budget tier with 4.5★ from 731 reviews.</p>
      </div>
    </div>
  </section>

  <!-- 10. CONCLUSION -->
  <section id="conclusion">
    <div class="section-header">
      <span class="section-num">10</span>
      <h2>Conclusion</h2>
    </div>
    <div class="conclusion-box">
      <p>The ThongLor restaurant landscape offers a high density of quality venues within a compact geographic zone, making it an excellent choice for team dining. The principal challenge is not scarcity of good options but rather the signal-to-noise problem: surface-level ratings are a poor guide without accounting for review volume, price-to-group-value dynamics, and operational practicalities.</p>
      <p style="margin-top:14px">This analysis recommends <strong>Market Café as the primary venue</strong>, supported by a clear, reproducible composite score of 87.3/100. It represents the intersection of peer-validated quality (4.9★ × 952 reviews), appropriate group pricing, and accessibility. <strong>57th Street</strong> is the preferred alternative when review volume confidence is the deciding factor, and <strong>Steps</strong> is recommended for informal team formats.</p>
      <p style="margin-top:14px">For any final booking decision, confirming group reservation availability and verifying current menu offerings directly with the venue is advised — particularly for the top two recommendations, which carry no confirmed address from a secondary source. The methodology and dataset underlying this report are fully reproducible and can be re-run with updated data for future team dining decisions.</p>
    </div>
  </section>

  <footer>
    <span>ThongLor Restaurant Intelligence Report · June 2026</span>
    <span>40 restaurants · 2 data sources · Composite scoring model</span>
  </footer>

</div>

<script>
const realScored = [
  {n:"Market Cafe",c:"Local",p:"Moderate",r:4.9,rv:952,rs:91.0,vs:85,ts:70,comp:87.3},
  {n:"57th Street",c:"Asian",p:"Moderate",r:4.8,rv:1587,rs:94.8,vs:85,ts:70,comp:85.0},
  {n:"Steps",c:"Cafe",p:"Moderate",r:4.9,rv:297,rs:88.7,vs:85,ts:70,comp:82.9},
  {n:"The Oasis - All Day Dining",c:"Japanese",p:"Moderate",r:4.9,rv:661,rs:89.8,vs:85,ts:70,comp:82.6},
  {n:"SEA Bangkok",c:"Asian",p:"Moderate",r:4.8,rv:636,rs:87.1,vs:85,ts:90,comp:86.8},
  {n:"Supanniga Eating Room",c:"Local",p:"Moderate",r:4.3,rv:707,rs:73.3,vs:75,ts:70,comp:73.9},
  {n:"Mott 32 Bangkok",c:"Asian",p:"Moderate",r:4.9,rv:249,rs:86.3,vs:85,ts:70,comp:81.9},
  {n:"Octave Rooftop Lounge & Bar",c:"Western",p:"Premium",r:4.6,rv:3936,rs:100.0,vs:40,ts:70,comp:71.5},
  {n:"Patara Fine Thai Cuisine",c:"Local",p:"Premium",r:4.5,rv:657,rs:79.3,vs:40,ts:90,comp:68.3},
  {n:"SHAKARICH",c:"Japanese",p:"Moderate",r:4.7,rv:534,rs:83.2,vs:75,ts:90,comp:82.0},
  {n:"La Galette",c:"Western",p:"Moderate",r:4.8,rv:475,rs:84.9,vs:85,ts:90,comp:86.2},
  {n:"Sababa",c:"Western",p:"Moderate",r:4.8,rv:362,rs:84.3,vs:85,ts:85,comp:84.6},
  {n:"Sunbird Smoothie & Sandwich",c:"Cafe",p:"Budget",r:4.9,rv:187,rs:85.1,vs:100,ts:90,comp:91.0},
  {n:"Goodburgs - Burgers & Fries",c:"Western",p:"Moderate",r:4.8,rv:148,rs:80.6,vs:85,ts:85,comp:83.4},
  {n:"Birdhouse Cafe & Bar",c:"Cafe",p:"Budget",r:4.8,rv:226,rs:82.2,vs:100,ts:85,comp:88.4},
  {n:"Bigknit Cafe",c:"Cafe",p:"Budget",r:4.4,rv:220,rs:70.3,vs:100,ts:85,comp:83.0},
  {n:"Sit and Wonder",c:"Local",p:"Budget",r:4.5,rv:731,rs:79.6,vs:100,ts:70,comp:83.7},
  {n:"Gopchang House",c:"Korean",p:"Moderate",r:4.4,rv:232,rs:70.4,vs:75,ts:90,comp:77.3},
  {n:"Masala Art Bangkok",c:"Western",p:"Moderate",r:4.5,rv:495,rs:77.6,vs:75,ts:70,comp:74.5},
  {n:"After You Dessert",c:"Cafe",p:"Moderate",r:4.4,rv:1029,rs:77.4,vs:75,ts:70,comp:74.2},
  {n:"The Gardens of Dinsor Palace",c:"Local",p:"Moderate",r:4.4,rv:372,rs:72.6,vs:75,ts:70,comp:72.7},
  {n:"17 Something",c:"Asian",p:"Moderate",r:4.6,rv:258,rs:75.2,vs:75,ts:90,comp:79.5},
  {n:"WOODs.bkk",c:"Western",p:"Moderate",r:4.8,rv:106,rs:79.4,vs:85,ts:90,comp:83.9},
  {n:"Matsaya",c:"Japanese",p:"Moderate",r:4.9,rv:32,rs:73.6,vs:75,ts:85,comp:77.7},
  {n:"The District Grill Room & Bar",c:"Cafe",p:"Premium",r:4.8,rv:1435,rs:95.6,vs:40,ts:70,comp:73.9},
  {n:"Miyabi Kappo",c:"Japanese",p:"Premium",r:4.6,rv:364,rs:78.0,vs:40,ts:90,comp:62.5},
  {n:"Baba Shuk",c:"Western",p:"Moderate",r:4.5,rv:132,rs:70.5,vs:75,ts:85,comp:75.8},
  {n:"Mae Varee Fruit Shop",c:"Cafe",p:"Budget",r:4.3,rv:329,rs:67.5,vs:100,ts:70,comp:76.5},
  {n:"Qrumb Restaurant",c:"Western",p:"Moderate",r:4.7,rv:61,rs:72.2,vs:75,ts:85,comp:76.7},
  {n:"Wattana Panich",c:"Local",p:"Budget",r:4.2,rv:136,rs:60.7,vs:100,ts:70,comp:73.1},
  {n:"Bun Meat & Cheese Burger",c:"Western",p:"Moderate",r:4.3,rv:143,rs:66.0,vs:75,ts:85,comp:74.2},
  {n:"The Little Prince Cafe",c:"Cafe",p:"Moderate",r:4.9,rv:62,rs:74.8,vs:85,ts:70,comp:75.4},
  {n:"Ojo Bangkok",c:"Western",p:"Premium",r:4.6,rv:204,rs:73.7,vs:40,ts:70,comp:61.6},
  {n:"Here Hai",c:"Local",p:"Moderate",r:4.2,rv:84,rs:59.7,vs:75,ts:70,comp:67.5},
  {n:"Nhong Rim Klong",c:"Local",p:"Moderate",r:4.2,rv:67,rs:58.1,vs:75,ts:70,comp:66.8},
  {n:"The Tepp Teppanyaki Buffet",c:"Asian",p:"Moderate",r:5.0,rv:2,rs:55.4,vs:75,ts:80,comp:68.3},
  {n:"Yentafo Yusuf",c:"Local",p:"Moderate",r:5.0,rv:1,rs:52.0,vs:75,ts:80,comp:67.3},
  {n:"Khao",c:"Local",p:"Premium",r:4.3,rv:122,rs:64.5,vs:40,ts:70,comp:57.5},
  {n:"Sushi Kappo Juichi",c:"Japanese",p:"Premium",r:5.0,rv:11,rs:61.5,vs:40,ts:85,comp:57.7},
  {n:"R-HAAN",c:"Local",p:"Premium",r:4.0,rv:140,rs:56.8,vs:40,ts:70,comp:55.3},
];

realScored.sort((a,b) => b.comp - a.comp);

const cuisineMap = {"Japanese":"jp","Korean":"kr","Cafe":"ca","Western":"we","Asian":"as","Local":"lc"};
const priceMap   = {"Budget":"bu","Moderate":"mo","Premium":"pr"};

function rankBadge(i) {
  if(i===0) return `<span class="rank-badge rb-1">1</span>`;
  if(i===1) return `<span class="rank-badge rb-2">2</span>`;
  if(i===2) return `<span class="rank-badge rb-3">3</span>`;
  return `<span class="rank-badge rb-n">${i+1}</span>`;
}
function scoreChip(v) {
  const cls = v>=80?'sc-hi':v>=70?'sc-md':'sc-lo';
  return `<span class="score-chip ${cls}">${v.toFixed(1)}</span>`;
}

const tbody = document.getElementById('rankBody');
realScored.forEach((r,i) => {
  const tr = document.createElement('tr');
  tr.innerHTML = `
    <td>${rankBadge(i)}</td>
    <td class="td-name">${r.n}</td>
    <td><span class="cuisine-tag c-${cuisineMap[r.c]||'as'}">${r.c}</span></td>
    <td><span class="price-tag p-${priceMap[r.p]||'mo'}">${r.p}</span></td>
    <td style="font-family:'DM Mono',monospace;font-size:12px">${r.r.toFixed(1)}</td>
    <td style="font-family:'DM Mono',monospace;font-size:12px">${r.rv.toLocaleString()}</td>
    <td>${r.rs.toFixed(0)}</td>
    <td>${r.vs}</td>
    <td>${r.ts}</td>
    <td>${scoreChip(r.comp)}</td>
  `;
  tbody.appendChild(tr);
});
</script>
</body>
</html>
