<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TANNN — Penerbitan Kunci Akses</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700&family=EB+Garamond:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root{
    --bg-deep:#120D09;
    --bg-panel:#1C1510;
    --bg-panel-2:#221A13;
    --line:#4A3B27;
    --line-soft:#332920;
    --gold:#C6A15B;
    --gold-bright:#E8C77E;
    --cream:#EFE6D8;
    --muted:#9C8F79;
    --muted-dim:#6E6353;
    --sage:#7E9B80;
    --wine:#9C4E52;
  }

  *{box-sizing:border-box;}

  body{
    margin:0;
    min-height:100vh;
    background:
      radial-gradient(ellipse 900px 600px at 50% 8%, rgba(198,161,91,0.10), transparent 60%),
      radial-gradient(ellipse 1200px 900px at 50% 100%, rgba(198,161,91,0.05), transparent 60%),
      var(--bg-deep);
    color:var(--cream);
    font-family:'EB Garamond', serif;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:48px 20px;
    position:relative;
    overflow-x:hidden;
  }

  /* halus garis guilloché di latar */
  body::before{
    content:"";
    position:fixed;
    inset:0;
    background-image:repeating-linear-gradient(115deg, rgba(198,161,91,0.035) 0px, rgba(198,161,91,0.035) 1px, transparent 1px, transparent 34px);
    pointer-events:none;
  }

  .plate{
    position:relative;
    width:100%;
    max-width:480px;
    background:linear-gradient(180deg, var(--bg-panel), var(--bg-panel-2));
    border:1px solid var(--line);
    padding:44px 38px 36px;
    animation:rise 0.7s cubic-bezier(.2,.8,.2,1) both;
  }

  .plate::before{
    content:"";
    position:absolute;
    inset:7px;
    border:1px solid var(--line-soft);
    pointer-events:none;
  }

  @keyframes rise{
    from{opacity:0; transform:translateY(10px) scale(.985);}
    to{opacity:1; transform:translateY(0) scale(1);}
  }

  @media (prefers-reduced-motion: reduce){
    .plate{animation:none;}
    *{transition:none !important;}
  }

  /* sudut bracket */
  .corner{position:absolute; width:16px; height:16px; z-index:2;}
  .corner.tl{top:-1px; left:-1px; border-top:2px solid var(--gold); border-left:2px solid var(--gold);}
  .corner.tr{top:-1px; right:-1px; border-top:2px solid var(--gold); border-right:2px solid var(--gold);}
  .corner.bl{bottom:-1px; left:-1px; border-bottom:2px solid var(--gold); border-left:2px solid var(--gold);}
  .corner.br{bottom:-1px; right:-1px; border-bottom:2px solid var(--gold); border-right:2px solid var(--gold);}

  .brand{
    text-align:center;
    margin-bottom:22px;
  }
  .brand h1{
    font-family:'Cinzel', serif;
    font-size:1.7rem;
    font-weight:600;
    letter-spacing:0.35em;
    margin:0;
    padding-left:0.35em; /* kompensasi letter-spacing agar tetap center */
    color:var(--gold-bright);
    text-shadow:0 0 22px rgba(198,161,91,0.25);
  }
  .brand p{
    margin:8px 0 0;
    font-size:0.82rem;
    letter-spacing:0.12em;
    color:var(--muted-dim);
    font-style:italic;
  }

  .hairline{
    height:1px;
    background:linear-gradient(90deg, transparent, var(--line) 20%, var(--line) 80%, transparent);
    margin:22px 0;
  }

  .status-row{
    display:flex;
    justify-content:center;
    margin-bottom:20px;
  }
  .status-pill{
    display:inline-flex;
    align-items:center;
    gap:8px;
    font-size:0.82rem;
    letter-spacing:0.04em;
    color:var(--muted);
    padding:5px 14px;
    border:1px solid var(--line);
  }
  .status-dot{width:6px; height:6px; border-radius:50%; background:var(--muted-dim); flex:none;}
  .status-pill.active .status-dot{background:var(--sage); box-shadow:0 0 6px var(--sage);}
  .status-pill.active{color:var(--sage);}
  .status-pill.expired .status-dot{background:var(--wine);}
  .status-pill.expired{color:var(--wine);}

  .key-display{
    text-align:center;
    min-height:72px;
    display:flex;
    align-items:center;
    justify-content:center;
    margin-bottom:6px;
  }
  .key-text{
    font-family:'Cinzel', serif;
    font-size:1.85rem;
    letter-spacing:0.14em;
    color:var(--gold-bright);
    word-break:break-word;
  }
  .key-text.dim{
    color:var(--muted-dim);
    font-size:1.4rem;
    letter-spacing:0.1em;
  }
  .used-tag{
    display:block;
    font-family:'EB Garamond', serif;
    font-size:0.75rem;
    letter-spacing:0.08em;
    color:var(--muted);
    margin-top:6px;
    font-style:italic;
  }

  .meta-row{
    display:flex;
    justify-content:space-between;
    font-size:0.8rem;
    color:var(--muted);
    margin:18px 4px 0;
  }
  .meta-row div{text-align:center; flex:1;}
  .meta-row span{display:block; color:var(--muted-dim); font-size:0.72rem; letter-spacing:0.08em; margin-bottom:3px;}

  .countdown{
    display:flex;
    justify-content:center;
    gap:10px;
    margin:22px 0 8px;
  }
  .seg{
    width:64px;
    text-align:center;
    padding:10px 0 8px;
    border:1px solid var(--line);
    background:rgba(0,0,0,0.15);
  }
  .seg b{
    display:block;
    font-family:'Cinzel', serif;
    font-size:1.25rem;
    color:var(--gold);
    font-weight:600;
  }
  .seg small{
    display:block;
    margin-top:4px;
    font-size:0.62rem;
    letter-spacing:0.1em;
    color:var(--muted-dim);
    text-transform:uppercase;
  }

  .progress-track{
    height:2px;
    background:var(--line-soft);
    margin:6px 4px 26px;
    position:relative;
    overflow:hidden;
  }
  .progress-fill{
    position:absolute;
    left:0; top:0; bottom:0;
    background:linear-gradient(90deg, var(--gold), var(--gold-bright));
    width:0%;
    transition:width 0.6s ease;
  }

  .empty-note{
    text-align:center;
    color:var(--muted);
    font-size:0.95rem;
    font-style:italic;
    margin:18px 0 26px;
    line-height:1.6;
  }

  button{
    font-family:'EB Garamond', serif;
    cursor:pointer;
  }

  .btn-primary{
    display:block;
    width:100%;
    padding:13px 0;
    background:transparent;
    border:1px solid var(--gold);
    color:var(--gold-bright);
    font-size:0.95rem;
    letter-spacing:0.1em;
    transition:background 0.25s ease, color 0.25s ease;
  }
  .btn-primary:hover:not(:disabled){
    background:var(--gold);
    color:#181008;
  }
  .btn-primary:disabled{
    border-color:var(--line);
    color:var(--muted-dim);
    cursor:default;
  }
  .btn-primary:focus-visible, .btn-secondary:focus-visible, input:focus-visible{
    outline:1px solid var(--gold-bright);
    outline-offset:3px;
  }

  .helper-text{
    text-align:center;
    font-size:0.78rem;
    color:var(--muted-dim);
    margin-top:10px;
    font-style:italic;
  }

  .redeem-title{
    font-size:1rem;
    letter-spacing:0.05em;
    color:var(--cream);
    margin:0 0 4px;
    text-align:center;
  }
  .redeem-desc{
    text-align:center;
    font-size:0.82rem;
    color:var(--muted);
    margin:0 0 16px;
    line-height:1.5;
  }

  .redeem-form{
    display:flex;
    gap:8px;
  }
  .redeem-form input{
    flex:1;
    min-width:0;
    background:rgba(0,0,0,0.18);
    border:1px solid var(--line);
    color:var(--cream);
    font-family:'EB Garamond', serif;
    font-size:0.95rem;
    letter-spacing:0.05em;
    padding:11px 12px;
  }
  .redeem-form input::placeholder{color:var(--muted-dim);}
  .btn-secondary{
    padding:0 20px;
    background:transparent;
    border:1px solid var(--line);
    color:var(--muted);
    font-size:0.85rem;
    letter-spacing:0.06em;
    transition:border-color 0.25s ease, color 0.25s ease;
  }
  .btn-secondary:hover{border-color:var(--gold); color:var(--gold-bright);}

  .feedback{
    margin-top:14px;
    padding-left:12px;
    border-left:2px solid var(--line);
    font-size:0.85rem;
    line-height:1.5;
    min-height:1.5em;
    color:var(--muted);
  }
  .feedback.ok{border-color:var(--sage); color:var(--sage);}
  .feedback.err{border-color:var(--wine); color:var(--wine);}

  .ledger{
    margin-top:8px;
  }
  .ledger h3{
    font-size:0.78rem;
    letter-spacing:0.12em;
    color:var(--muted-dim);
    text-transform:uppercase;
    margin:0 0 10px;
    text-align:center;
  }
  .ledger ul{list-style:none; margin:0; padding:0;}
  .ledger li{
    display:flex;
    justify-content:space-between;
    gap:10px;
    font-size:0.82rem;
    color:var(--muted);
    padding:7px 0;
    border-bottom:1px solid var(--line-soft);
  }
  .ledger li:last-child{border-bottom:none;}
  .ledger li .lk{color:var(--cream); letter-spacing:0.04em;}
  .ledger li .lstat{font-style:italic; color:var(--muted-dim); white-space:nowrap;}

  .foot-note{
    text-align:center;
    font-size:0.72rem;
    color:var(--muted-dim);
    margin-top:26px;
    letter-spacing:0.03em;
  }

  @media (max-width:420px){
    .plate{padding:34px 22px 28px;}
    .brand h1{font-size:1.35rem; letter-spacing:0.26em;}
    .key-text{font-size:1.4rem;}
    .seg{width:52px; padding:8px 0 6px;}
    .seg b{font-size:1.05rem;}
    .redeem-form{flex-direction:column;}
    .btn-secondary{padding:11px 0;}
  }
</style>
</head>
<body>

<div class="plate">
  <span class="corner tl"></span><span class="corner tr"></span>
  <span class="corner bl"></span><span class="corner br"></span>

  <div class="brand">
    <h1>TANNN</h1>
    <p>Sistem Penerbitan Kunci Akses</p>
  </div>

  <div class="status-row">
    <span class="status-pill" id="statusPill">
      <span class="status-dot"></span>
      <span id="statusText">Belum ada kunci</span>
    </span>
  </div>

  <div class="key-display">
    <span class="key-text dim" id="keyText">Tannn-•••-•••</span>
  </div>
  <span class="used-tag" id="usedTag" style="display:none;">Kunci ini telah digunakan</span>

  <div id="issuedBlock" style="display:none;">
    <div class="meta-row">
      <div><span>Diterbitkan</span><b id="issuedAt">—</b></div>
      <div><span>Kadaluarsa pada</span><b id="expiresAt">—</b></div>
    </div>

    <div class="countdown">
      <div class="seg"><b id="segDays">00</b><small>Hari</small></div>
      <div class="seg"><b id="segHours">00</b><small>Jam</small></div>
      <div class="seg"><b id="segMins">00</b><small>Menit</small></div>
      <div class="seg"><b id="segSecs">00</b><small>Detik</small></div>
    </div>
    <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
  </div>

  <p class="empty-note" id="emptyNote">
    Belum ada kunci yang diterbitkan. Klik tombol di bawah untuk menerbitkan kunci akses pertama Anda.
  </p>

  <button class="btn-primary" id="generateBtn">Terbitkan Kunci Baru</button>
  <p class="helper-text" id="helperText" style="display:none;">
    Kunci baru dapat diterbitkan setelah kunci saat ini kadaluarsa.
  </p>

  <div class="hairline"></div>

  <p class="redeem-title">Gunakan Kunci</p>
  <p class="redeem-desc">Masukkan kunci untuk menandainya terpakai. Setiap kunci hanya berlaku satu kali pemakaian.</p>
  <div class="redeem-form">
    <input type="text" id="redeemInput" placeholder="Tannn-000-000" autocomplete="off" spellcheck="false">
    <button class="btn-secondary" id="redeemBtn">Gunakan</button>
  </div>
  <div class="feedback" id="feedback"></div>

  <div class="hairline" id="ledgerDivider" style="display:none;"></div>
  <div class="ledger" id="ledgerBlock" style="display:none;">
    <h3>Riwayat Kunci</h3>
    <ul id="ledgerList"></ul>
  </div>

  <p class="foot-note">Kunci disimpan secara lokal pada peramban ini.</p>
</div>

<script>
(function(){
  const STORAGE_KEY = 'tannn_vault_state_v1';
  const HISTORY_KEY = 'tannn_vault_history_v1';
  const LIFETIME_MS = 14 * 24 * 60 * 60 * 1000; // 14 hari

  const el = {
    statusPill: document.getElementById('statusPill'),
    statusText: document.getElementById('statusText'),
    keyText: document.getElementById('keyText'),
    usedTag: document.getElementById('usedTag'),
    issuedBlock: document.getElementById('issuedBlock'),
    issuedAt: document.getElementById('issuedAt'),
    expiresAt: document.getElementById('expiresAt'),
    segDays: document.getElementById('segDays'),
    segHours: document.getElementById('segHours'),
    segMins: document.getElementById('segMins'),
    segSecs: document.getElementById('segSecs'),
    progressFill: document.getElementById('progressFill'),
    emptyNote: document.getElementById('emptyNote'),
    generateBtn: document.getElementById('generateBtn'),
    helperText: document.getElementById('helperText'),
    redeemInput: document.getElementById('redeemInput'),
    redeemBtn: document.getElementById('redeemBtn'),
    feedback: document.getElementById('feedback'),
    ledgerDivider: document.getElementById('ledgerDivider'),
    ledgerBlock: document.getElementById('ledgerBlock'),
    ledgerList: document.getElementById('ledgerList'),
  };

  function loadState(){
    try{
      const raw = localStorage.getItem(STORAGE_KEY);
      return raw ? JSON.parse(raw) : null;
    }catch(e){ return null; }
  }
  function saveState(state){
    localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
  }
  function loadHistory(){
    try{
      const raw = localStorage.getItem(HISTORY_KEY);
      return raw ? JSON.parse(raw) : [];
    }catch(e){ return []; }
  }
  function saveHistory(list){
    localStorage.setItem(HISTORY_KEY, JSON.stringify(list.slice(0,5)));
  }

  function randomDigits(n){
    const max = Math.pow(10, n);
    return String(Math.floor(Math.random()*max)).padStart(n,'0');
  }
  function generateKeyString(){
    return 'Tannn-' + randomDigits(3) + '-' + randomDigits(3);
  }

  function fmtDateTime(ts){
    const d = new Date(ts);
    return d.toLocaleString('id-ID', {
      day:'2-digit', month:'short', year:'numeric',
      hour:'2-digit', minute:'2-digit'
    });
  }

  function pad2(n){ return String(n).padStart(2,'0'); }

  let state = loadState();
  let timer = null;

  function isExpired(s){
    return !s || Date.now() >= s.expiresAt;
  }

  function render(){
    const now = Date.now();

    if(!state){
      // belum pernah ada kunci
      el.statusPill.className = 'status-pill';
      el.statusText.textContent = 'Belum ada kunci';
      el.keyText.textContent = 'Tannn-•••-•••';
      el.keyText.classList.add('dim');
      el.usedTag.style.display = 'none';
      el.issuedBlock.style.display = 'none';
      el.emptyNote.style.display = 'block';
      el.generateBtn.disabled = false;
      el.generateBtn.textContent = 'Terbitkan Kunci Baru';
      el.helperText.style.display = 'none';
      return;
    }

    const expired = isExpired(state);
    el.keyText.classList.remove('dim');
    el.keyText.textContent = state.key;
    el.emptyNote.style.display = 'none';
    el.issuedBlock.style.display = 'block';
    el.issuedAt.textContent = fmtDateTime(state.issuedAt);
    el.expiresAt.textContent = fmtDateTime(state.expiresAt);
    el.usedTag.style.display = state.used ? 'block' : 'none';

    if(!expired){
      el.statusPill.className = 'status-pill active';
      el.statusText.textContent = 'Kunci aktif';
      el.generateBtn.disabled = true;
      el.generateBtn.textContent = 'Kunci Masih Aktif';
      el.helperText.style.display = 'block';

      const remaining = state.expiresAt - now;
      const days = Math.floor(remaining / 86400000);
      const hours = Math.floor((remaining % 86400000) / 3600000);
      const mins = Math.floor((remaining % 3600000) / 60000);
      const secs = Math.floor((remaining % 60000) / 1000);
      el.segDays.textContent = pad2(days);
      el.segHours.textContent = pad2(hours);
      el.segMins.textContent = pad2(mins);
      el.segSecs.textContent = pad2(secs);

      const elapsed = now - state.issuedAt;
      const pct = Math.min(100, Math.max(0, (elapsed / LIFETIME_MS) * 100));
      el.progressFill.style.width = pct + '%';
    } else {
      el.statusPill.className = 'status-pill expired';
      el.statusText.textContent = 'Kunci kadaluarsa';
      el.generateBtn.disabled = false;
      el.generateBtn.textContent = 'Terbitkan Kunci Baru';
      el.helperText.style.display = 'none';
      el.segDays.textContent = '00';
      el.segHours.textContent = '00';
      el.segMins.textContent = '00';
      el.segSecs.textContent = '00';
      el.progressFill.style.width = '100%';
    }

    renderLedger();
  }

  function renderLedger(){
    const hist = loadHistory();
    if(hist.length === 0){
      el.ledgerDivider.style.display = 'none';
      el.ledgerBlock.style.display = 'none';
      return;
    }
    el.ledgerDivider.style.display = 'block';
    el.ledgerBlock.style.display = 'block';
    el.ledgerList.innerHTML = '';
    hist.forEach(function(h){
      const li = document.createElement('li');
      const left = document.createElement('span');
      left.className = 'lk';
      left.textContent = h.key;
      const right = document.createElement('span');
      right.className = 'lstat';
      right.textContent = h.status;
      li.appendChild(left);
      li.appendChild(right);
      el.ledgerList.appendChild(li);
    });
  }

  function archiveCurrent(){
    if(!state) return;
    const hist = loadHistory();
    hist.unshift({
      key: state.key,
      status: state.used ? 'Terpakai, kadaluarsa' : 'Tidak dipakai, kadaluarsa'
    });
    saveHistory(hist);
  }

  function handleGenerate(){
    if(state && !isExpired(state)) return;
    if(state && isExpired(state)) archiveCurrent();

    const now = Date.now();
    state = {
      key: generateKeyString(),
      issuedAt: now,
      expiresAt: now + LIFETIME_MS,
      used: false,
      usedAt: null
    };
    saveState(state);
    el.feedback.textContent = '';
    el.feedback.className = 'feedback';
    render();
  }

  function setFeedback(msg, kind){
    el.feedback.textContent = msg;
    el.feedback.className = 'feedback ' + (kind || '');
  }

  function handleRedeem(){
    const input = el.redeemInput.value.trim();
    if(!input){
      setFeedback('Masukkan kunci terlebih dahulu.', 'err');
      return;
    }
    if(!state){
      setFeedback('Belum ada kunci aktif untuk digunakan.', 'err');
      return;
    }
    if(isExpired(state)){
      setFeedback('Kunci sudah kadaluarsa dan tidak dapat digunakan.', 'err');
      return;
    }
    if(input !== state.key){
      setFeedback('Kunci tidak cocok dengan kunci aktif saat ini.', 'err');
      return;
    }
    if(state.used){
      setFeedback('Kunci ini sudah pernah digunakan sebelumnya.', 'err');
      return;
    }
    state.used = true;
    state.usedAt = Date.now();
    saveState(state);
    setFeedback('Kunci berhasil digunakan. Kunci ini tidak dapat digunakan kembali.', 'ok');
    el.redeemInput.value = '';
    render();
  }

  el.generateBtn.addEventListener('click', handleGenerate);
  el.redeemBtn.addEventListener('click', handleRedeem);
  el.redeemInput.addEventListener('keydown', function(e){
    if(e.key === 'Enter') handleRedeem();
  });

  render();
  timer = setInterval(function(){
    if(state && isExpired(state)){
      // status baru saja berubah menjadi kadaluarsa, cukup render ulang tanpa interval detik
      render();
    } else if(state){
      render();
    }
  }, 1000);
})();
</script>

</body>
</html>
