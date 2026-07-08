
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
<title>London Term Ledger</title>
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Term Ledger">
<meta name="theme-color" content="#28433A">
<link rel="apple-touch-icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 180 180'%3E%3Crect width='180' height='180' rx='34' fill='%2328433A'/%3E%3Crect x='0' y='0' width='180' height='180' rx='34' fill='none' stroke='%23A9823C' stroke-width='2'/%3E%3Ctext x='90' y='78' font-family='Georgia,serif' font-size='58' font-weight='700' fill='%23F7F1E3' text-anchor='middle'%3E%C2%A3%3C/text%3E%3Cline x1='46' y1='104' x2='134' y2='104' stroke='%23A9823C' stroke-width='2'/%3E%3Cline x1='46' y1='118' x2='134' y2='118' stroke='%23A9823C' stroke-width='2'/%3E%3Cline x1='46' y1='132' x2='104' y2='132' stroke='%23A9823C' stroke-width='2'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=IBM+Plex+Mono:wght@400;500;600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#1B2A41;
    --ink-soft:#3B4A5E;
    --paper:#F7F1E3;
    --paper-2:#F1E9D5;
    --paper-line:#DED0AC;
    --cover:#28433A;
    --cover-2:#1B2E27;
    --gold:#A9823C;
    --gold-soft:#C7A96B;
    --stamp-red:#B4392C;
    --stamp-green:#2E6B4F;
    --shadow: 0 30px 60px -20px rgba(20,25,20,0.45);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    min-height:100vh;
    background: radial-gradient(circle at 20% 0%, #33413A 0%, #1E2723 55%, #14201B 100%);
    font-family:'Inter',sans-serif;
    color:var(--ink);
    padding: 28px 16px 60px;
    display:flex;
    justify-content:center;
  }
  .book{
    width:100%;
    max-width:860px;
    background:var(--paper);
    border-radius:14px;
    box-shadow: var(--shadow);
    overflow:hidden;
    position:relative;
    animation: openBook .7s cubic-bezier(.2,.8,.25,1) both;
  }
  .book:before{
    content:"";
    position:absolute; left:0; top:0; bottom:0; width:14px;
    background:linear-gradient(90deg, rgba(0,0,0,.35), rgba(0,0,0,0));
    z-index:5;
  }
  @keyframes openBook{
    from{ opacity:0; transform: perspective(1200px) rotateY(-6deg) scale(.97); }
    to{ opacity:1; transform: perspective(1200px) rotateY(0deg) scale(1); }
  }

  /* ---------- Cover ---------- */
  .cover{
    background: linear-gradient(160deg, var(--cover) 0%, var(--cover-2) 100%);
    color: var(--paper);
    padding: 26px 30px 22px;
    position:relative;
  }
  .cover-top{ display:flex; justify-content:space-between; align-items:flex-start; gap:12px; }
  .cover-mark{ font-family:'Fraunces',serif; font-weight:700; font-size:12px; letter-spacing:.22em; color:var(--gold); text-transform:uppercase; }
  .cover-title{ font-family:'Fraunces',serif; font-weight:600; font-size:30px; line-height:1.05; margin:6px 0 4px; }
  .cover-sub{ font-size:12.5px; color:#CBD6C9; letter-spacing:.03em; }
  .gear-btn{
    background:rgba(247,241,227,0.1); border:1px solid rgba(247,241,227,.28); color:var(--paper);
    width:34px;height:34px;border-radius:50%; cursor:pointer; display:flex; align-items:center; justify-content:center;
    flex:none; transition:background .15s ease;
  }
  .gear-btn:hover{ background:rgba(247,241,227,.22); }

  .month-nav{ display:flex; align-items:center; justify-content:center; gap:18px; margin-top:22px; }
  .month-nav button{
    background:none;border:none;color:var(--paper); cursor:pointer; opacity:.75; padding:6px;
    display:flex; align-items:center; justify-content:center; transition:opacity .15s ease, transform .15s ease;
  }
  .month-nav button:hover{ opacity:1; transform:scale(1.08); }
  .month-label{ font-family:'Fraunces',serif; font-size:20px; letter-spacing:.06em; min-width:190px; text-align:center; }
  .month-label small{ display:block; font-family:'Inter',sans-serif; font-size:10.5px; letter-spacing:.14em; color:var(--gold); margin-top:2px; text-transform:uppercase;}

  /* ---------- Settings drawer ---------- */
  .settings{
    background: var(--cover-2); color:var(--paper); padding:0 30px; max-height:0; overflow:hidden;
    transition: max-height .35s ease, padding .35s ease;
  }
  .settings.open{ max-height:600px; padding:20px 30px 26px; }
  .settings h4{ font-family:'Fraunces',serif; font-size:14px; letter-spacing:.05em; color:var(--gold); margin:14px 0 8px; text-transform:uppercase; font-weight:600;}
  .settings h4:first-child{ margin-top:0; }
  .settings-grid{ display:grid; grid-template-columns:1fr 1fr; gap:10px 16px; }
  .settings-row{ display:flex; align-items:center; justify-content:space-between; gap:10px; font-size:12.5px; padding:5px 0; border-bottom:1px dashed rgba(247,241,227,.15); }
  .settings-row input[type=number], .settings-row input[type=date]{
    width:100px; background:rgba(247,241,227,.08); border:1px solid rgba(247,241,227,.25); color:var(--paper);
    border-radius:6px; padding:4px 7px; font-family:'IBM Plex Mono',monospace; font-size:12px; text-align:right;
  }
  .settings-row input[type=date]{ width:130px; text-align:left; }
  .toggle-row{ display:flex; align-items:center; justify-content:space-between; padding:8px 0; font-size:12.5px; }
  .switch{ position:relative; width:38px; height:20px; }
  .switch input{ opacity:0; width:0; height:0; }
  .slider{ position:absolute; inset:0; background:rgba(247,241,227,.22); border-radius:20px; cursor:pointer; transition:.2s; }
  .slider:before{ content:""; position:absolute; height:14px; width:14px; left:3px; top:3px; background:var(--paper); border-radius:50%; transition:.2s; }
  .switch input:checked + .slider{ background:var(--gold); }
  .switch input:checked + .slider:before{ transform:translateX(18px); }

  /* ---------- Statement summary ---------- */
  .summary{ display:grid; grid-template-columns:1fr 1fr 1fr; gap:0; border-bottom:1px solid var(--paper-line); }
  .stat{ padding:20px 22px; border-right:1px solid var(--paper-line); }
  .stat:last-child{ border-right:none; }
  .stat-label{ font-size:10.5px; letter-spacing:.13em; text-transform:uppercase; color:var(--ink-soft); margin-bottom:6px; }
  .stat-value{ font-family:'IBM Plex Mono',monospace; font-size:22px; font-weight:600; }
  .stat-sub{ font-size:11px; color:var(--ink-soft); margin-top:3px; }
  .stat.net .stat-value.pos{ color:var(--stamp-green); }
  .stat.net .stat-value.neg{ color:var(--stamp-red); }
  .stamp{
    display:inline-block; margin-top:8px; padding:3px 10px; border:2px solid currentColor; border-radius:4px;
    font-family:'Fraunces',serif; font-weight:700; font-size:10.5px; letter-spacing:.12em; transform:rotate(-4deg);
  }
  .stamp.ok{ color:var(--stamp-green); }
  .stamp.over{ color:var(--stamp-red); }

  /* ---------- New entry slip ---------- */
  .slip{ padding:20px 30px 8px; border-bottom:2px dashed var(--paper-line); }
  .slip h3{ font-family:'Fraunces',serif; font-size:15px; margin:0 0 12px; letter-spacing:.02em; }
  .type-toggle{ display:flex; gap:0; margin-bottom:12px; border:1px solid var(--ink); border-radius:8px; overflow:hidden; width:fit-content; }
  .type-toggle button{
    border:none; background:var(--paper); color:var(--ink); font-family:'Inter',sans-serif; font-size:12.5px; font-weight:600;
    padding:8px 18px; cursor:pointer; transition:background .15s ease, color .15s ease;
  }
  .type-toggle button.active.debit{ background:var(--ink); color:var(--paper); }
  .type-toggle button.active.credit{ background:var(--stamp-green); color:var(--paper); }

  .slip-form{ display:grid; grid-template-columns: 130px 1fr 110px; gap:10px; align-items:end; margin-bottom:12px;}
  .field label{ display:block; font-size:10.5px; letter-spacing:.08em; text-transform:uppercase; color:var(--ink-soft); margin-bottom:4px; }
  .field input, .field select{
    width:100%; padding:8px 10px; border:1px solid var(--paper-line); border-radius:7px; background:#fff;
    font-family:'Inter',sans-serif; font-size:13px; color:var(--ink);
  }
  .field input[type=number]{ font-family:'IBM Plex Mono',monospace; }
  .chips{ display:flex; flex-wrap:wrap; gap:6px; margin-bottom:12px; }
  .chip{
    padding:6px 12px; border-radius:20px; font-size:12px; font-weight:500; cursor:pointer; border:1.5px solid transparent;
    color:#fff; opacity:.55; transition:opacity .15s ease, transform .1s ease; user-select:none;
  }
  .chip:hover{ opacity:.8; }
  .chip.active{ opacity:1; border-color:var(--ink); transform:scale(1.03); }
  .note-row{ display:flex; gap:10px; align-items:end; }
  .note-row .field{ flex:1; }
  .post-btn{
    background:var(--cover); color:var(--paper); border:none; border-radius:7px; padding:9px 20px; font-size:13px;
    font-weight:600; cursor:pointer; display:flex; align-items:center; gap:6px; transition:background .15s ease, transform .08s ease;
    font-family:'Inter',sans-serif;
  }
  .post-btn:hover{ background:var(--cover-2); }
  .post-btn:active{ transform:scale(.97); }
  .err{ color:var(--stamp-red); font-size:11.5px; margin:-4px 0 10px; min-height:14px; }

  /* ---------- Ledger register ---------- */
  .ledger{ padding: 6px 30px 4px; }
  .ledger h3{ font-family:'Fraunces',serif; font-size:15px; margin:16px 0 8px; }
  table.reg{ width:100%; border-collapse:collapse; font-size:13px; }
  table.reg thead th{
    text-align:left; font-size:10.5px; letter-spacing:.1em; text-transform:uppercase; color:var(--ink-soft);
    border-bottom:1px solid var(--ink); padding:6px 6px; font-weight:600;
  }
  table.reg thead th.num, table.reg td.num{ text-align:right; }
  table.reg tbody tr{ border-bottom:1px solid var(--paper-line); }
  table.reg tbody tr.bf td{ font-style:italic; color:var(--ink-soft); }
  table.reg td{ padding:8px 6px; vertical-align:top; }
  .cat-tag{ display:inline-block; padding:2px 8px; border-radius:10px; font-size:10.5px; color:#fff; margin-right:6px; }
  .desc-note{ color:var(--ink-soft); font-size:11.5px; }
  .mono{ font-family:'IBM Plex Mono',monospace; }
  .credit-val{ color:var(--stamp-green); }
  .debit-val{ color:var(--stamp-red); }
  .del-btn{
    background:none; border:none; color:var(--ink-soft); cursor:pointer; opacity:0; transition:opacity .12s ease, color .12s ease;
    padding:2px; font-size:14px; line-height:1;
  }
  table.reg tbody tr:hover .del-btn{ opacity:.55; }
  .del-btn:hover{ opacity:1 !important; color:var(--stamp-red); }
  .empty-row td{ text-align:center; color:var(--ink-soft); font-style:italic; padding:22px 0; }

  /* ---------- Statement of accounts (categories + goals) ---------- */
  .statement{ padding: 8px 30px 26px; display:grid; grid-template-columns:1.4fr 1fr; gap:26px; }
  @media (max-width:640px){ .statement{ grid-template-columns:1fr; } .slip-form{ grid-template-columns:1fr; } .summary{ grid-template-columns:1fr; } .stat{ border-right:none; border-bottom:1px solid var(--paper-line);} }
  .statement h3{ font-family:'Fraunces',serif; font-size:15px; margin:10px 0 10px; }
  .cat-row{ margin-bottom:10px; }
  .cat-row-top{ display:flex; justify-content:space-between; font-size:12px; margin-bottom:4px; }
  .cat-row-top .name{ font-weight:600; }
  .bar-track{ height:7px; background:var(--paper-2); border-radius:6px; overflow:hidden; border:1px solid var(--paper-line); }
  .bar-fill{ height:100%; border-radius:6px; transition:width .3s ease; }
  .goal-card{
    background:var(--paper-2); border:1px solid var(--paper-line); border-radius:10px; padding:12px 14px; margin-bottom:10px;
  }
  .goal-top{ display:flex; justify-content:space-between; align-items:center; font-size:12.5px; font-weight:600; }
  .goal-check{ font-size:11px; padding:2px 8px; border-radius:10px; font-weight:700; letter-spacing:.04em; }
  .goal-check.met{ background:rgba(46,107,79,.15); color:var(--stamp-green); }
  .goal-check.pending{ background:rgba(180,57,44,.12); color:var(--stamp-red); }
  .goal-sub{ font-size:11px; color:var(--ink-soft); margin-top:4px; }

  .footer-note{ padding:14px 30px 26px; font-size:11px; color:var(--ink-soft); border-top:1px solid var(--paper-line); line-height:1.5; }
</style>
</head>
<body>
<div id="app"></div>
<script>
(function(){

  /* ---------------- constants ---------------- */
  var CATS = [
    {key:'food', label:'Food', budget:220, color:'#6B7A3F'},
    {key:'transport', label:'Transport', budget:40, color:'#3F6B7A'},
    {key:'mobile', label:'Mobile', budget:10, color:'#7A5C3F'},
    {key:'gym', label:'Gym', budget:15, color:'#7A3F5C'},
    {key:'personalCare', label:'Personal Care', budget:30, color:'#3F5C7A'},
    {key:'laundry', label:'Laundry & Household', budget:20, color:'#5C7A3F'},
    {key:'study', label:'Study/Printing', budget:20, color:'#7A6B3F'},
    {key:'social', label:'Social & Misc.', budget:20, color:'#5C3F7A'},
    {key:'other', label:'Other/Emergency', budget:30, color:'#7A3F3F'}
  ];
  var SHADOW_EMI = {
    '2026-09':36,'2026-10':123,'2026-11':123,'2026-12':123,
    '2027-01':242,'2027-02':242,'2027-03':242,
    '2027-04':356,'2027-05':356,'2027-06':356,'2027-07':356,
    '2027-08':395,'2027-09':395
  };
  var MONTH_NAMES = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];

  var defaultSettings = {
    fx: 127.3,
    arrivalDate: '2026-09-10',
    selfFund: false,
    contributionMonthly: 1023.59,
    contributionEndMonth: '2027-08',
    gradVisaSaving: 500,
    futureShadowEmi: 395,
    categories: CATS
  };

  var state = {
    loaded:false,
    entries: [],
    settings: JSON.parse(JSON.stringify(defaultSettings)),
    selectedMonth: '2026-09',
    entryType: 'expense',
    entryCategory: 'food',
    settingsOpen:false,
    draft: { date: todayStr(), amount:'', note:'', source:'' }
  };

  /* ---------------- storage (browser localStorage — works standalone, offline, no Claude session needed) ---------------- */
  function loadData(){
    try{
      var raw = localStorage.getItem('ledger-entries');
      state.entries = raw ? JSON.parse(raw) : [];
    }catch(err){ state.entries = []; }
    try{
      var raw2 = localStorage.getItem('ledger-settings');
      if(raw2){
        var parsed = JSON.parse(raw2);
        state.settings = Object.assign({}, defaultSettings, parsed);
        if(!state.settings.categories || !state.settings.categories.length) state.settings.categories = CATS;
      }
    }catch(err){ /* keep defaults */ }
    state.loaded = true;
    state.selectedMonth = monthKey(state.settings.arrivalDate);
    render();
  }
  function saveEntries(){
    try{ localStorage.setItem('ledger-entries', JSON.stringify(state.entries)); }catch(e){ console.warn('Could not save entries', e); }
  }
  function saveSettings(){
    try{ localStorage.setItem('ledger-settings', JSON.stringify(state.settings)); }catch(e){ console.warn('Could not save settings', e); }
  }

  /* ---------------- helpers ---------------- */
  function monthKey(d){ return d.slice(0,7); }
  function todayStr(){
    var d = new Date();
    var y = d.getFullYear(), m = String(d.getMonth()+1).padStart(2,'0'), day = String(d.getDate()).padStart(2,'0');
    return y+'-'+m+'-'+day;
  }
  function daysInMonth(ym){
    var parts = ym.split('-'); var y = +parts[0], m = +parts[1];
    return new Date(y, m, 0).getDate();
  }
  function fmtMonth(ym){
    var parts = ym.split('-'); var y = +parts[0], m = +parts[1];
    return MONTH_NAMES[m-1] + ' ' + y;
  }
  function addMonths(ym, n){
    var parts = ym.split('-'); var y = +parts[0], m = +parts[1];
    var total = (m-1) + n;
    var y2 = y + Math.floor(total/12);
    var m2 = ((total % 12) + 12) % 12 + 1;
    return y2 + '-' + String(m2).padStart(2,'0');
  }
  function money(n){
    var neg = n < 0;
    var v = Math.abs(n).toLocaleString('en-GB', {minimumFractionDigits:2, maximumFractionDigits:2});
    return (neg?'-':'') + '£' + v;
  }
  function shadowEmiFor(ym){
    if(SHADOW_EMI[ym] !== undefined) return SHADOW_EMI[ym];
    var firstKnown = Object.keys(SHADOW_EMI).sort()[0];
    if(ym < firstKnown) return SHADOW_EMI[firstKnown];
    return state.settings.futureShadowEmi;
  }
  function prorationFactor(ym){
    var arrivalMonth = monthKey(state.settings.arrivalDate);
    if(ym !== arrivalMonth) return 1;
    var day = +state.settings.arrivalDate.split('-')[2];
    var dim = daysInMonth(ym);
    return Math.max(0, (dim - day + 1) / dim);
  }
  function categoryBudgetTotal(ym){
    var sum = state.settings.categories.reduce(function(a,c){return a+c.budget;},0);
    return sum * prorationFactor(ym);
  }
  function incomeTargetFor(ym){
    var factor = prorationFactor(ym);
    var base = (state.settings.categories.reduce(function(a,c){return a+c.budget;},0) + shadowEmiFor(ym) + state.settings.gradVisaSaving) * factor;
    if(state.settings.selfFund && ym <= state.settings.contributionEndMonth){
      base += state.settings.contributionMonthly;
    }
    return base;
  }
  function uid(){ return Date.now().toString(36) + Math.random().toString(36).slice(2,7); }

  /* ---------------- derived data ---------------- */
  function entriesSorted(){
    return state.entries.slice().sort(function(a,b){
      if(a.date !== b.date) return a.date < b.date ? -1 : 1;
      return a.id < b.id ? -1 : 1;
    });
  }
  function withRunningBalance(){
    var sorted = entriesSorted();
    var bal = 0;
    return sorted.map(function(e){
      bal += (e.type === 'income' ? e.amount : -e.amount);
      return Object.assign({}, e, {balanceAfter: bal});
    });
  }
  function monthEntries(ym){
    return withRunningBalance().filter(function(e){ return monthKey(e.date) === ym; });
  }
  function balanceBroughtForward(ym){
    var all = withRunningBalance();
    var before = all.filter(function(e){ return monthKey(e.date) < ym; });
    return before.length ? before[before.length-1].balanceAfter : 0;
  }

  /* ---------------- render ---------------- */
  function render(){
    if(!state.loaded){
      document.getElementById('app').innerHTML = '<div style="color:#eee;padding:60px;text-align:center;font-family:Inter,sans-serif;">Opening your ledger…</div>';
      return;
    }
    var ym = state.selectedMonth;
    var mEntries = monthEntries(ym);
    var spent = mEntries.filter(function(e){return e.type==='expense';}).reduce(function(a,e){return a+e.amount;},0);
    var earned = mEntries.filter(function(e){return e.type==='income';}).reduce(function(a,e){return a+e.amount;},0);
    var budgetTotal = categoryBudgetTotal(ym);
    var incomeTarget = incomeTargetFor(ym);
    var net = earned - spent;
    var overBudget = spent > budgetTotal;
    var bf = balanceBroughtForward(ym);

    var spentByCat = {};
    state.settings.categories.forEach(function(c){ spentByCat[c.key] = 0; });
    mEntries.forEach(function(e){ if(e.type==='expense' && spentByCat[e.category] !== undefined) spentByCat[e.category] += e.amount; });

    var shadowTarget = shadowEmiFor(ym) * prorationFactor(ym);
    var gradTarget = state.settings.gradVisaSaving * prorationFactor(ym);
    var goalsMet = net >= (shadowTarget + gradTarget);

    var html = '';
    html += '<div class="book">';

    /* cover */
    html += '<div class="cover">';
    html += '  <div class="cover-top">';
    html += '    <div><div class="cover-mark">London Term Ledger</div><div class="cover-title">Daily Account Register</div>';
    html += '    <div class="cover-sub">LSE MSc Finance · tracking from arrival in London</div></div>';
    html += '    <button class="gear-btn" data-action="toggle-settings" title="Settings">'+gearIcon()+'</button>';
    html += '  </div>';
    html += '  <div class="month-nav">';
    html += '    <button data-action="prev-month">'+chevron('left')+'</button>';
    html += '    <div class="month-label">'+fmtMonth(ym)+'<small>'+monthIndexLabel(ym)+'</small></div>';
    html += '    <button data-action="next-month">'+chevron('right')+'</button>';
    html += '  </div>';
    html += '</div>';

    /* settings */
    html += '<div class="settings'+(state.settingsOpen?' open':'')+'">';
    html += settingsHtml();
    html += '</div>';

    /* summary */
    html += '<div class="summary">';
    html += statBlock('Spent this month', money(spent), 'of '+money(budgetTotal)+' budget', overBudget ? '<span class="stamp over">OVER BUDGET</span>' : '<span class="stamp ok">ON TRACK</span>');
    html += statBlock('Earned this month', money(earned), 'target '+money(incomeTarget), earned >= incomeTarget ? '<span class="stamp ok">TARGET MET</span>' : '<span class="stamp over">BELOW TARGET</span>');
    html += '  <div class="stat net">';
    html += '    <div class="stat-label">Net position</div>';
    html += '    <div class="stat-value '+(net>=0?'pos':'neg')+'">'+money(net)+'</div>';
    html += '    <div class="stat-sub">balance b/f '+money(bf)+' → '+money(bf+net)+'</div>';
    html += '  </div>';
    html += '</div>';

    /* slip */
    html += '<div class="slip">';
    html += '  <h3>New Entry</h3>';
    html += '  <div class="type-toggle">';
    html += '    <button class="'+(state.entryType==='expense'?'active debit':'')+'" data-action="set-type" data-type="expense">Debit (Spend)</button>';
    html += '    <button class="'+(state.entryType==='income'?'active credit':'')+'" data-action="set-type" data-type="income">Credit (Earned)</button>';
    html += '  </div>';
    html += '  <div class="slip-form">';
    html += '    <div class="field"><label>Date</label><input type="date" id="f-date" value="'+state.draft.date+'"></div>';
    if(state.entryType === 'expense'){
      html += '    <div class="field"><label>Category</label><div style="padding-top:4px;">'+chipsHtml()+'</div></div>';
    } else {
      html += '    <div class="field"><label>Source</label><input type="text" id="f-source" placeholder="e.g. Café shift, Tutoring" value="'+escapeHtml(state.draft.source)+'"></div>';
    }
    html += '    <div class="field"><label>Amount (£)</label><input type="number" id="f-amount" placeholder="0.00" step="0.01" min="0" value="'+state.draft.amount+'"></div>';
    html += '  </div>';
    html += '  <div class="note-row">';
    html += '    <div class="field"><label>Note (optional)</label><input type="text" id="f-note" placeholder="Add a short note…" value="'+escapeHtml(state.draft.note)+'"></div>';
    html += '    <button class="post-btn" data-action="add-entry">'+plusIcon()+' Post Entry</button>';
    html += '  </div>';
    html += '  <div class="err" id="f-err"></div>';
    html += '</div>';

    /* ledger register */
    html += '<div class="ledger"><h3>Register — '+fmtMonth(ym)+'</h3>';
    html += '<table class="reg"><thead><tr><th>Date</th><th>Description</th><th class="num">Debit</th><th class="num">Credit</th><th class="num">Balance</th><th></th></tr></thead><tbody>';
    html += '<tr class="bf"><td colspan="4">Balance brought forward</td><td class="num mono">'+money(bf)+'</td><td></td></tr>';
    if(mEntries.length === 0){
      html += '<tr class="empty-row"><td colspan="6">No entries yet this month — post one above to begin.</td></tr>';
    } else {
      mEntries.forEach(function(e){
        var catInfo = state.settings.categories.find(function(c){return c.key===e.category;});
        var descLabel = e.type==='expense' ? (catInfo?catInfo.label:e.category) : (e.source || 'Income');
        var chipColor = e.type==='expense' ? (catInfo?catInfo.color:'#7A3F3F') : '#2E6B4F';
        html += '<tr data-id="'+e.id+'">';
        html += '  <td class="mono">'+e.date.slice(8,10)+' '+MONTH_NAMES[+e.date.slice(5,7)-1]+'</td>';
        html += '  <td><span class="cat-tag" style="background:'+chipColor+'">'+descLabel+'</span>'+(e.note?'<div class="desc-note">'+escapeHtml(e.note)+'</div>':'')+'</td>';
        html += '  <td class="num mono debit-val">'+(e.type==='expense'?money(e.amount):'')+'</td>';
        html += '  <td class="num mono credit-val">'+(e.type==='income'?money(e.amount):'')+'</td>';
        html += '  <td class="num mono">'+money(e.balanceAfter)+'</td>';
        html += '  <td><button class="del-btn" data-action="delete-entry" data-id="'+e.id+'">✕</button></td>';
        html += '</tr>';
      });
    }
    html += '</tbody></table></div>';

    /* statement: categories + goals */
    html += '<div class="statement">';
    html += '  <div><h3>Category Statement</h3>';
    state.settings.categories.forEach(function(c){
      var sp = spentByCat[c.key]||0;
      var bud = c.budget * prorationFactor(ym);
      var pct = bud>0 ? Math.min(100, (sp/bud)*100) : 0;
      var over = sp > bud;
      html += '<div class="cat-row">';
      html += '  <div class="cat-row-top"><span class="name">'+c.label+'</span><span class="mono">'+money(sp)+' / '+money(bud)+'</span></div>';
      html += '  <div class="bar-track"><div class="bar-fill" style="width:'+pct+'%;background:'+(over?'var(--stamp-red)':c.color)+'"></div></div>';
      html += '</div>';
    });
    html += '  </div>';
    html += '  <div><h3>Savings Goals</h3>';
    html += goalCard('Shadow EMI saving', shadowTarget, net, shadowTarget<=net);
    html += goalCard('Graduate visa saving', gradTarget, Math.max(0,net-shadowTarget), (net-shadowTarget)>=gradTarget);
    if(state.settings.selfFund && ym <= state.settings.contributionEndMonth){
      html += goalCard('Contribution self-fund (this month)', state.settings.contributionMonthly, Math.max(0,net-shadowTarget-gradTarget), (net-shadowTarget-gradTarget) >= state.settings.contributionMonthly);
    }
    html += '  </div>';
    html += '</div>';

    html += '<div class="footer-note">Entries are saved in this browser on this device only (not synced to other devices). '
          + 'Budgets, targets and the arrival-month proration all come from your London financial plan — adjust them any time in Settings.</div>';

    html += '</div>'; // .book
    document.getElementById('app').innerHTML = html;
    attachEvents();
  }

  function statBlock(label, value, sub, badge){
    return '<div class="stat"><div class="stat-label">'+label+'</div><div class="stat-value">'+value+'</div><div class="stat-sub">'+sub+'</div>'+badge+'</div>';
  }
  function goalCard(label, target, progress, met){
    var pct = target>0 ? Math.min(100,(progress/target)*100) : 0;
    return '<div class="goal-card"><div class="goal-top"><span>'+label+'</span><span class="goal-check '+(met?'met':'pending')+'">'+(met?'ON TRACK':'PENDING')+'</span></div>'
      + '<div class="bar-track" style="margin-top:8px;"><div class="bar-fill" style="width:'+pct+'%;background:'+(met?'var(--stamp-green)':'var(--gold)')+'"></div></div>'
      + '<div class="goal-sub">target '+money(target)+' from this month\'s net position</div></div>';
  }
  function chipsHtml(){
    return '<div class="chips">' + state.settings.categories.map(function(c){
      return '<span class="chip '+(state.entryCategory===c.key?'active':'')+'" style="background:'+c.color+'" data-action="set-category" data-cat="'+c.key+'">'+c.label+'</span>';
    }).join('') + '</div>';
  }
  function monthIndexLabel(ym){
    var arrivalMonth = monthKey(state.settings.arrivalDate);
    var diff = (function(a,b){
      var pa=a.split('-').map(Number), pb=b.split('-').map(Number);
      return (pb[0]-pa[0])*12 + (pb[1]-pa[1]);
    })(arrivalMonth, ym);
    if(diff < 0) return 'Before arrival';
    return 'Month ' + (diff+1) + ' in London';
  }
  function settingsHtml(){
    var s = state.settings;
    var h = '';
    h += '<h4>Rates & Dates</h4><div class="settings-grid">';
    h += '<div class="settings-row"><span>GBP → INR rate</span><input type="number" step="0.01" id="s-fx" value="'+s.fx+'"></div>';
    h += '<div class="settings-row"><span>Arrival date</span><input type="date" id="s-arrival" value="'+s.arrivalDate+'"></div>';
    h += '<div class="settings-row"><span>Grad visa saving/mo</span><input type="number" step="1" id="s-gradvisa" value="'+s.gradVisaSaving+'"></div>';
    h += '<div class="settings-row"><span>Shadow EMI (future mo.)</span><input type="number" step="1" id="s-futureemi" value="'+s.futureShadowEmi+'"></div>';
    h += '</div>';
    h += '<h4>Contribution Funding</h4>';
    h += '<div class="toggle-row"><span>I\'m self-funding the 27.35% contribution</span><label class="switch"><input type="checkbox" id="s-selffund" '+(s.selfFund?'checked':'')+'><span class="slider"></span></label></div>';
    h += '<div class="settings-grid">';
    h += '<div class="settings-row"><span>Contribution £/month</span><input type="number" step="0.01" id="s-contrib" value="'+s.contributionMonthly+'"></div>';
    h += '<div class="settings-row"><span>Contribution ends</span><input type="date" id="s-contribend" value="'+s.contributionEndMonth+'-01"></div>';
    h += '</div>';
    h += '<h4>Category Budgets (£/month)</h4><div class="settings-grid">';
    s.categories.forEach(function(c, i){
      h += '<div class="settings-row"><span>'+c.label+'</span><input type="number" step="1" data-cat-budget="'+c.key+'" value="'+c.budget+'"></div>';
    });
    h += '</div>';
    return h;
  }
  function chevron(dir){
    var d = dir==='left' ? 'M15 18l-6-6 6-6' : 'M9 18l6-6-6-6';
    return '<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="'+d+'"/></svg>';
  }
  function plusIcon(){
    return '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg>';
  }
  function gearIcon(){
    return '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 11-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 11-2.83-2.83l.06-.06A1.65 1.65 0 004.6 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 112.83-2.83l.06.06A1.65 1.65 0 009 4.6a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09A1.65 1.65 0 0015 4.6a1.65 1.65 0 001.82-.33l.06-.06a2 2 0 112.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>';
  }
  function escapeHtml(s){
    return s.replace(/[&<>"']/g, function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c];});
  }

  /* ---------------- events ---------------- */
  function attachEvents(){
    var app = document.getElementById('app');
    app.onclick = function(ev){
      var t = ev.target.closest('[data-action]');
      if(!t) return;
      var action = t.getAttribute('data-action');
      if(action === 'toggle-settings'){ state.settingsOpen = !state.settingsOpen; render(); }
      else if(action === 'prev-month'){ state.selectedMonth = addMonths(state.selectedMonth, -1); render(); }
      else if(action === 'next-month'){ state.selectedMonth = addMonths(state.selectedMonth, 1); render(); }
      else if(action === 'set-type'){ state.entryType = t.getAttribute('data-type'); render(); }
      else if(action === 'set-category'){ state.entryCategory = t.getAttribute('data-cat'); render(); }
      else if(action === 'add-entry'){ handleAddEntry(); }
      else if(action === 'delete-entry'){ handleDelete(t.getAttribute('data-id')); }
    };

    // settings inputs
    var byId = function(id){ return document.getElementById(id); };
    bindNum('s-fx', function(v){ state.settings.fx = v; });
    bindVal('s-arrival', function(v){ state.settings.arrivalDate = v; state.selectedMonth = monthKey(v); });
    bindNum('s-gradvisa', function(v){ state.settings.gradVisaSaving = v; });
    bindNum('s-futureemi', function(v){ state.settings.futureShadowEmi = v; });
    var sf = byId('s-selffund');
    if(sf) sf.onchange = function(){ state.settings.selfFund = sf.checked; saveSettings(); render(); };
    bindNum('s-contrib', function(v){ state.settings.contributionMonthly = v; });
    var ce = byId('s-contribend');
    if(ce) ce.onchange = function(){ state.settings.contributionEndMonth = monthKey(ce.value); saveSettings(); render(); };

    document.querySelectorAll('[data-cat-budget]').forEach(function(inp){
      inp.onchange = function(){
        var key = inp.getAttribute('data-cat-budget');
        var cat = state.settings.categories.find(function(c){return c.key===key;});
        if(cat){ cat.budget = parseFloat(inp.value)||0; saveSettings(); render(); }
      };
    });

    // keep the in-progress entry draft in sync without forcing a re-render (avoids losing focus/typed text)
    var fDate = byId('f-date'); if(fDate) fDate.oninput = function(){ state.draft.date = fDate.value; };
    var fAmount = byId('f-amount'); if(fAmount) fAmount.oninput = function(){ state.draft.amount = fAmount.value; };
    var fNote = byId('f-note'); if(fNote) fNote.oninput = function(){ state.draft.note = fNote.value; };
    var fSource = byId('f-source'); if(fSource) fSource.oninput = function(){ state.draft.source = fSource.value; };

    function bindNum(id, fn){
      var el = byId(id);
      if(el) el.onchange = function(){ fn(parseFloat(el.value)||0); saveSettings(); render(); };
    }
    function bindVal(id, fn){
      var el = byId(id);
      if(el) el.onchange = function(){ fn(el.value); saveSettings(); render(); };
    }
  }

  function handleAddEntry(){
    var errEl = document.getElementById('f-err');
    errEl.textContent = '';
    var date = document.getElementById('f-date').value;
    var amountEl = document.getElementById('f-amount');
    var amount = parseFloat(amountEl.value);
    var note = document.getElementById('f-note').value.trim();
    if(!date){ errEl.textContent = 'Please choose a date.'; return; }
    if(!amount || amount <= 0){ errEl.textContent = 'Enter an amount greater than £0.'; return; }
    var entry = { id: uid(), date: date, type: state.entryType, amount: amount, note: note };
    if(state.entryType === 'expense'){
      entry.category = state.entryCategory;
    } else {
      var src = document.getElementById('f-source').value.trim();
      if(!src){ errEl.textContent = 'Add a short source for this income.'; return; }
      entry.source = src;
    }
    state.entries.push(entry);
    saveEntries();
    state.selectedMonth = monthKey(date);
    state.draft = { date: todayStr(), amount:'', note:'', source:'' };
    render();
  }
  function handleDelete(id){
    state.entries = state.entries.filter(function(e){ return e.id !== id; });
    saveEntries();
    render();
  }

  loadData();
})();
</script>
</body>
</html>
