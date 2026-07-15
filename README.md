# testresults
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Natijalar daftari</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,600;9..144,700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #121826;
    --bg-2: #0d121c;
    --panel: #1c2536;
    --panel-2: #212d40;
    --line: #2e3b52;
    --ink: #eef1f0;
    --ink-dim: #93a0b5;
    --brass: #c9a227;
    --brass-dim: #8a7325;
    --pass: #5fae95;
    --fail: #c15a44;
    --shadow: 0 24px 50px -25px rgba(0,0,0,0.65);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background: radial-gradient(ellipse at top, #182236 0%, var(--bg) 55%, var(--bg-2) 100%);
    color: var(--ink);
    font-family: 'Inter', sans-serif;
    min-height:100vh;
  }
  .wrap{ max-width: 880px; margin: 0 auto; padding: 36px 20px 70px; }

  .brand{
    text-align:center;
    margin-bottom: 26px;
  }
  .brand .eyebrow{
    font-family:'IBM Plex Mono', monospace;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    font-size: 11px;
    color: var(--brass);
    margin-bottom: 8px;
  }
  .brand h1{
    font-family:'Fraunces', serif;
    font-weight: 600;
    font-size: clamp(26px, 5vw, 38px);
    margin: 0;
    letter-spacing: -0.01em;
  }

  /* ---- ledger index tabs ---- */
  .tabs{
    display:flex;
    justify-content:center;
    gap: 2px;
    margin: 30px 0 0;
    position: relative;
    z-index: 2;
  }
  .tabs button{
    font-family:'IBM Plex Mono', monospace;
    font-size: 13px;
    font-weight:600;
    letter-spacing: 0.04em;
    background: var(--panel);
    border: 1px solid var(--line);
    border-bottom: none;
    color: var(--ink-dim);
    padding: 12px 26px 14px;
    cursor:pointer;
    clip-path: polygon(10px 0, 100% 0, calc(100% - 10px) 100%, 0 100%);
    transition: color 0.2s ease, background 0.2s ease;
  }
  .tabs button.active{
    background: var(--brass);
    color: #241c05;
  }
  .tabs button:not(.active):hover{ color: var(--ink); }

  .stage{
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 4px 14px 14px 14px;
    box-shadow: var(--shadow);
    padding: 30px;
    position: relative;
    z-index: 1;
  }

  h2.section-title{
    font-family:'Fraunces', serif;
    font-weight: 600;
    font-size: 19px;
    margin: 0 0 4px;
  }
  p.section-sub{
    color: var(--ink-dim);
    font-size: 13px;
    margin: 0 0 22px;
  }

  /* ---- search ---- */
  .search-row{
    display:flex;
    gap: 10px;
    margin-bottom: 6px;
  }
  input[type="text"], input[type="password"], input[type="number"]{
    background: var(--panel-2);
    border: 1px solid var(--line);
    border-radius: 8px;
    color: var(--ink);
    font-family: 'Inter', sans-serif;
    font-size: 15px;
    padding: 12px 14px;
    outline: none;
    width: 100%;
    transition: border-color 0.2s ease;
  }
  input:focus{ border-color: var(--brass-dim); }
  input::placeholder{ color: #5c6a80; }

  button.primary{
    font-family:'IBM Plex Mono', monospace;
    font-weight:600;
    font-size: 13px;
    background: var(--brass);
    color: #241c05;
    border: none;
    border-radius: 8px;
    padding: 0 22px;
    cursor:pointer;
    white-space:nowrap;
    transition: filter 0.15s ease;
  }
  button.primary:hover{ filter: brightness(1.08); }
  button.primary:disabled{ opacity: 0.5; cursor:not-allowed; }

  button.ghost{
    font-family:'IBM Plex Mono', monospace;
    font-size: 12px;
    background: transparent;
    color: var(--ink-dim);
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 9px 16px;
    cursor:pointer;
  }
  button.ghost:hover{ color: var(--ink); border-color: var(--brass-dim); }

  button.danger{
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    background: transparent;
    color: var(--fail);
    border: 1px solid #4a2a24;
    border-radius: 6px;
    padding: 6px 10px;
    cursor:pointer;
  }
  button.danger:hover{ background: rgba(193,90,68,0.12); }

  .hint{
    font-size: 12px;
    color: var(--ink-dim);
    margin-top: 10px;
  }

  /* ---- result cards ---- */
  .result-card{
    background: var(--panel-2);
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 20px 22px;
    margin-top: 22px;
  }
  .result-head{
    display:flex;
    justify-content: space-between;
    align-items: baseline;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 14px;
    padding-bottom: 14px;
    border-bottom: 1px dashed var(--line);
  }
  .result-head .name{
    font-family:'Fraunces', serif;
    font-weight:600;
    font-size: 20px;
  }
  .result-head .group{
    font-family:'IBM Plex Mono', monospace;
    font-size: 12.5px;
    color: var(--brass);
  }
  table.grades{
    width:100%;
    border-collapse: collapse;
  }
  table.grades th{
    text-align:left;
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    color: var(--ink-dim);
    padding: 6px 8px;
    border-bottom: 1px solid var(--line);
  }
  table.grades td{
    padding: 10px 8px;
    font-size: 14px;
    border-bottom: 1px solid var(--line);
  }
  table.grades tr:last-child td{ border-bottom:none; }
  td.score-cell{ font-family:'IBM Plex Mono', monospace; font-weight:600; }

  .stamp{
    font-family:'IBM Plex Mono', monospace;
    font-size: 10.5px;
    font-weight:700;
    letter-spacing: 0.06em;
    display:inline-block;
    border: 2px solid var(--pass);
    color: var(--pass);
    border-radius: 5px;
    padding: 2px 8px;
    transform: rotate(-4deg);
  }
  .stamp.fail{ border-color: var(--fail); color: var(--fail); }

  .avg-row{
    display:flex;
    justify-content: space-between;
    margin-top: 14px;
    padding-top: 14px;
    border-top: 1px solid var(--line);
    font-family:'IBM Plex Mono', monospace;
    font-size: 13px;
    color: var(--ink-dim);
  }
  .avg-row b{ color: var(--ink); font-size: 16px; }

  .empty{
    text-align:center;
    padding: 30px 10px;
    color: var(--ink-dim);
    font-size: 14px;
  }

  /* ---- admin ---- */
  .lock-wrap{
    max-width: 340px;
    margin: 10px auto 0;
    text-align:center;
  }
  .lock-wrap .search-row{ margin-top: 16px; }
  .admin-topbar{
    display:flex;
    justify-content: space-between;
    align-items:center;
    margin-bottom: 22px;
  }
  .admin-section{
    margin-top: 28px;
    padding-top: 24px;
    border-top: 1px dashed var(--line);
  }
  .admin-section:first-of-type{ margin-top: 0; padding-top: 0; border-top:none; }
  .inline-form{
    display:flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  .inline-form input{ width: auto; flex: 1; min-width: 140px; }

  .chip-list{
    display:flex; flex-wrap:wrap; gap: 8px; margin-top: 14px;
  }
  .chip{
    display:flex; align-items:center; gap: 8px;
    background: var(--panel-2);
    border: 1px solid var(--line);
    border-radius: 999px;
    padding: 6px 8px 6px 14px;
    font-family:'IBM Plex Mono', monospace;
    font-size: 12.5px;
  }
  .chip button{ background:none; border:none; color: var(--fail); cursor:pointer; font-size:13px; padding: 2px 4px; }

  .grade-table-wrap{ overflow-x:auto; margin-top: 14px; }
  table.admin-grades{ border-collapse: collapse; width: 100%; min-width: 480px; }
  table.admin-grades th, table.admin-grades td{
    border: 1px solid var(--line);
    padding: 8px;
    font-size: 13px;
    text-align:center;
  }
  table.admin-grades th{
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    color: var(--brass);
    background: var(--panel-2);
  }
  table.admin-grades td.name-cell{ text-align:left; font-weight:600; white-space:nowrap; }
  table.admin-grades td.group-cell{ text-align:left; color: var(--ink-dim); font-family:'IBM Plex Mono', monospace; font-size:12px; white-space:nowrap; }
  table.admin-grades input[type="number"]{
    padding: 6px; text-align:center; width: 64px;
  }

  .save-bar{
    display:flex; align-items:center; gap: 12px;
    margin-top: 18px;
  }
  .save-status{ font-size: 12px; color: var(--ink-dim); font-family:'IBM Plex Mono', monospace; }

  footer{
    text-align:center;
    margin-top: 26px;
    font-size: 11.5px;
    color: var(--ink-dim);
    line-height:1.6;
  }

  @media (max-width: 520px){
    .stage{ padding: 22px 18px; }
    .search-row{ flex-direction:column; }
    button.primary{ padding: 12px 22px; }
  }
</style>
</head>
<body>
<div class="wrap">
  <div class="brand">
    <div class="eyebrow">Natijalar daftari</div>
    <h1>Talabalar test natijalari</h1>
  </div>

  <div id="setupNotice" style="display:none; background:#3a2a12; border:1px solid var(--brass-dim); color:#f0d896; border-radius:10px; padding:14px 18px; font-size:13px; margin-bottom:20px; text-align:center;">
    ⚠ Firebase hali sozlanmagan. Fayl ichidagi <code>firebaseConfig</code> qismini to'ldiring, aks holda natijalar saqlanmaydi.
  </div>

  <div class="tabs">
    <button class="tab-btn active" data-tab="student">Natijalar</button>
    <button class="tab-btn" data-tab="admin">Admin</button>
  </div>

  <!-- STUDENT VIEW -->
  <div class="stage" id="studentStage">
    <h2 class="section-title">Natijangizni toping</h2>
    <p class="section-sub">Ismingiz yoki guruh nomingizni kiriting.</p>
    <div class="search-row">
      <input type="text" id="searchInput" placeholder="Masalan: Aziza Karimova yoki 21-IF-14">
      <button class="primary" id="searchBtn">Qidirish</button>
    </div>
    <div class="hint" id="studentHint"></div>
    <div id="resultsArea"></div>
  </div>

  <!-- ADMIN VIEW -->
  <div class="stage" id="adminStage" style="display:none;">

    <div id="adminLockView">
      <div class="lock-wrap">
        <h2 class="section-title" id="lockTitle">Admin panel</h2>
        <p class="section-sub" id="lockSub">Kirish uchun email va parolni kiriting.</p>
        <div class="search-row" style="flex-direction:column;">
          <input type="text" id="adminEmailInput" placeholder="Email" autocomplete="username">
          <input type="password" id="adminPwInput" placeholder="Parol" autocomplete="current-password">
          <button class="primary" id="adminPwBtn" style="width:100%;">Kirish</button>
        </div>
        <div class="hint" id="lockHint"></div>
      </div>
    </div>

    <div id="adminPanelView" style="display:none;">
      <div class="admin-topbar">
        <h2 class="section-title" style="margin:0;">Admin panel</h2>
        <button class="ghost" id="logoutBtn">Chiqish</button>
      </div>

      <div class="admin-section">
        <h2 class="section-title">Modullar</h2>
        <p class="section-sub">Har bir ustun bitta unit/modul natijasini bildiradi.</p>
        <div class="inline-form">
          <input type="text" id="unitInput" placeholder="Masalan: 1-modul">
          <button class="primary" id="addUnitBtn">Qo'shish</button>
        </div>
        <div class="chip-list" id="unitChips"></div>
      </div>

      <div class="admin-section">
        <h2 class="section-title">Talaba qo'shish</h2>
        <div class="inline-form">
          <input type="text" id="studentNameInput" placeholder="Ism familiya">
          <input type="text" id="studentGroupInput" placeholder="Guruh nomi">
          <button class="primary" id="addStudentBtn">Qo'shish</button>
        </div>
      </div>

      <div class="admin-section">
        <h2 class="section-title">Natijalarni kiritish</h2>
        <p class="section-sub">Har bir katakka ballni yozing (0–100), so'ng saqlang.</p>
        <div class="grade-table-wrap">
          <table class="admin-grades" id="adminGradesTable"></table>
        </div>
        <div class="save-bar">
          <button class="primary" id="saveBtn">Saqlash</button>
          <span class="save-status" id="saveStatus"></span>
        </div>
      </div>
    </div>
  </div>

  <footer>
    Ma'lumotlar Firebase'da saqlanadi — sayt havolasiga ega bo'lgan har kim natijalarni ko'ra oladi.<br>
    Natijalarni faqat admin sifatida ro'yxatdan o'tgan foydalanuvchi kirita oladi.
  </footer>
</div>

<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-auth-compat.js"></script>
<script>
/* =====================================================================
   FIREBASE SOZLAMALARI — bu yerni o'zingizning Firebase konfiguratsiyangiz
   bilan almashtiring. Firebase Console → Project settings → General →
   "Your apps" → Web app (</>) dan olinadi.
   ===================================================================== */
const firebaseConfig = {
  apiKey: "AIzaSyCOaqLaZ3GFhednIjIjO-TylWbULmyW8DA",
  authDomain: "test-results-e7431.firebaseapp.com",
  projectId: "test-results-e7431",
  storageBucket: "test-results-e7431.firebasestorage.app",
  messagingSenderId: "507789683076",
  appId: "1:507789683076:web:69796322dacac312ff55d1"
};

const firebaseNotConfigured = firebaseConfig.apiKey === "YOUR_API_KEY";
let db = null;
let auth = null;
if(!firebaseNotConfigured){
  firebase.initializeApp(firebaseConfig);
  db = firebase.firestore();
  auth = firebase.auth();
}

const GRADEBOOK_DOC = 'gradebook';
const PASS_THRESHOLD = 60;

let data = { units: [], students: [] };
let isAdminLoggedIn = false;
let dataLoaded = false;

const tabBtns = document.querySelectorAll('.tab-btn');
const studentStage = document.getElementById('studentStage');
const adminStage = document.getElementById('adminStage');
const adminLockView = document.getElementById('adminLockView');
const adminPanelView = document.getElementById('adminPanelView');

async function loadData(){
  if(firebaseNotConfigured){ dataLoaded = true; return; }
  try{
    const snap = await db.collection('gradebook').doc(GRADEBOOK_DOC).get();
    if(snap.exists){
      const d = snap.data();
      data.units = Array.isArray(d.units) ? d.units : [];
      data.students = Array.isArray(d.students) ? d.students : [];
    }
  }catch(e){
    data = { units: [], students: [] };
  }
  dataLoaded = true;
}

async function saveData(){
  if(firebaseNotConfigured) return false;
  try{
    await db.collection('gradebook').doc(GRADEBOOK_DOC).set({
      units: data.units,
      students: data.students
    });
    return true;
  }catch(e){
    return false;
  }
}

/* ---------------- tabs ---------------- */
tabBtns.forEach(btn => {
  btn.addEventListener('click', () => switchTab(btn.dataset.tab));
});

function switchTab(tab){
  tabBtns.forEach(b => b.classList.toggle('active', b.dataset.tab === tab));
  studentStage.style.display = tab === 'student' ? 'block' : 'none';
  adminStage.style.display = tab === 'admin' ? 'block' : 'none';
  if(tab === 'admin'){
    initAdminLock();
  }
}

/* ---------------- student view ---------------- */
const searchInput = document.getElementById('searchInput');
const searchBtn = document.getElementById('searchBtn');
const resultsArea = document.getElementById('resultsArea');
const studentHint = document.getElementById('studentHint');

async function runSearch(){
  const q = searchInput.value.trim().toLowerCase();
  resultsArea.innerHTML = '';
  if(!q){
    studentHint.textContent = "Iltimos, ism yoki guruh nomini kiriting.";
    return;
  }
  studentHint.textContent = 'Qidirilmoqda…';
  if(!dataLoaded) await loadData();
  studentHint.textContent = '';

  const matches = data.students.filter(s =>
    s.name.toLowerCase().includes(q) || s.group.toLowerCase().includes(q)
  );

  if(matches.length === 0){
    resultsArea.innerHTML = '<div class="empty">Hech narsa topilmadi. Ism yoki guruh nomini tekshirib ko\'ring.</div>';
    return;
  }

  matches.forEach(s => resultsArea.appendChild(renderResultCard(s)));
}

function renderResultCard(student){
  const card = document.createElement('div');
  card.className = 'result-card';

  const head = document.createElement('div');
  head.className = 'result-head';
  head.innerHTML = `<span class="name">${escapeHtml(student.name)}</span><span class="group">${escapeHtml(student.group)}</span>`;
  card.appendChild(head);

  if(data.units.length === 0){
    card.innerHTML += '<div class="empty">Hali modullar qo\'shilmagan.</div>';
    return card;
  }

  const table = document.createElement('table');
  table.className = 'grades';
  table.innerHTML = `<thead><tr><th>Modul</th><th>Ball</th><th>Holat</th></tr></thead>`;
  const tbody = document.createElement('tbody');

  let sum = 0, count = 0;
  data.units.forEach(unit => {
    const raw = student.scores ? student.scores[unit] : undefined;
    const hasScore = raw !== undefined && raw !== null && raw !== '';
    const score = hasScore ? Number(raw) : null;
    if(hasScore && !isNaN(score)){ sum += score; count++; }

    const tr = document.createElement('tr');
    const statusHtml = !hasScore
      ? '<span style="color:var(--ink-dim);font-size:12.5px;">—</span>'
      : (score >= PASS_THRESHOLD
          ? '<span class="stamp">O\'TDI</span>'
          : '<span class="stamp fail">QAYTA</span>');
    tr.innerHTML = `<td>${escapeHtml(unit)}</td><td class="score-cell">${hasScore ? score : '—'}</td><td>${statusHtml}</td>`;
    tbody.appendChild(tr);
  });
  table.appendChild(tbody);
  card.appendChild(table);

  const avgRow = document.createElement('div');
  avgRow.className = 'avg-row';
  const avg = count > 0 ? (sum / count).toFixed(1) : '—';
  avgRow.innerHTML = `<span>O'rtacha ball</span><b>${avg}</b>`;
  card.appendChild(avgRow);

  return card;
}

function escapeHtml(str){
  const d = document.createElement('div');
  d.textContent = str;
  return d.innerHTML;
}

searchBtn.addEventListener('click', runSearch);
searchInput.addEventListener('keydown', e => { if(e.key === 'Enter') runSearch(); });

/* ---------------- admin: lock / login (Firebase Auth) ---------------- */
const lockTitle = document.getElementById('lockTitle');
const lockSub = document.getElementById('lockSub');
const lockHint = document.getElementById('lockHint');
const adminEmailInput = document.getElementById('adminEmailInput');
const adminPwInput = document.getElementById('adminPwInput');
const adminPwBtn = document.getElementById('adminPwBtn');
const logoutBtn = document.getElementById('logoutBtn');

function initAdminLock(){
  if(firebaseNotConfigured){
    lockTitle.textContent = "Firebase sozlanmagan";
    lockSub.textContent = "Fayl ichidagi firebaseConfig qismini to'ldiring (yuqoridagi izohga qarang).";
    adminEmailInput.style.display = 'none';
    adminPwInput.style.display = 'none';
    adminPwBtn.style.display = 'none';
    return;
  }
  if(isAdminLoggedIn){
    showAdminPanel();
    return;
  }
  adminLockView.style.display = 'block';
  adminPanelView.style.display = 'none';
  lockTitle.textContent = "Admin panel";
  lockSub.textContent = "Kirish uchun email va parolni kiriting.";
  lockHint.textContent = '';
  adminPwInput.value = '';
}

adminPwBtn.addEventListener('click', handleAdminLogin);
adminPwInput.addEventListener('keydown', e => { if(e.key === 'Enter') handleAdminLogin(); });
adminEmailInput.addEventListener('keydown', e => { if(e.key === 'Enter') handleAdminLogin(); });

async function handleAdminLogin(){
  const email = adminEmailInput.value.trim();
  const pw = adminPwInput.value;
  if(!email || !pw){
    lockHint.textContent = "Email va parolni kiriting.";
    return;
  }
  adminPwBtn.disabled = true;
  lockHint.textContent = 'Tekshirilmoqda…';
  try{
    await auth.signInWithEmailAndPassword(email, pw);
    // holat o'zgarishi onAuthStateChanged orqali ushlanadi
  }catch(e){
    lockHint.textContent = "Email yoki parol noto'g'ri.";
  }
  adminPwBtn.disabled = false;
}

logoutBtn.addEventListener('click', async () => {
  if(auth) await auth.signOut();
});

if(auth){
  auth.onAuthStateChanged(user => {
    isAdminLoggedIn = !!user;
    // Faqat Admin bo'limi ochiq bo'lganda ko'rinishni yangilaymiz
    if(adminStage.style.display !== 'none'){
      initAdminLock();
    }
  });
}

async function showAdminPanel(){
  adminLockView.style.display = 'none';
  adminPanelView.style.display = 'block';
  if(!dataLoaded) await loadData();
  renderUnitChips();
  renderAdminGradeTable();
}

/* ---------------- admin: units ---------------- */
const unitInput = document.getElementById('unitInput');
const addUnitBtn = document.getElementById('addUnitBtn');
const unitChips = document.getElementById('unitChips');

addUnitBtn.addEventListener('click', async () => {
  const name = unitInput.value.trim();
  if(!name) return;
  if(data.units.includes(name)){ unitInput.value=''; return; }
  data.units.push(name);
  unitInput.value = '';
  renderUnitChips();
  renderAdminGradeTable();
  await saveData();
});

function renderUnitChips(){
  unitChips.innerHTML = '';
  data.units.forEach(unit => {
    const chip = document.createElement('div');
    chip.className = 'chip';
    chip.innerHTML = `<span>${escapeHtml(unit)}</span>`;
    const del = document.createElement('button');
    del.textContent = '✕';
    del.title = "O'chirish";
    del.addEventListener('click', async () => {
      if(!confirm(`"${unit}" modulini o'chirasizmi? Unga tegishli barcha ballar ham o'chadi.`)) return;
      data.units = data.units.filter(u => u !== unit);
      data.students.forEach(s => { if(s.scores) delete s.scores[unit]; });
      renderUnitChips();
      renderAdminGradeTable();
      await saveData();
    });
    chip.appendChild(del);
    unitChips.appendChild(chip);
  });
  if(data.units.length === 0){
    unitChips.innerHTML = '<span class="hint">Hali modul qo\'shilmagan.</span>';
  }
}

/* ---------------- admin: students ---------------- */
const studentNameInput = document.getElementById('studentNameInput');
const studentGroupInput = document.getElementById('studentGroupInput');
const addStudentBtn = document.getElementById('addStudentBtn');

addStudentBtn.addEventListener('click', async () => {
  const name = studentNameInput.value.trim();
  const group = studentGroupInput.value.trim();
  if(!name || !group) return;
  data.students.push({ id: 's' + Date.now() + Math.floor(Math.random()*1000), name, group, scores: {} });
  studentNameInput.value = '';
  studentGroupInput.value = '';
  renderAdminGradeTable();
  await saveData();
});

/* ---------------- admin: grade table ---------------- */
const adminGradesTable = document.getElementById('adminGradesTable');
const saveBtn = document.getElementById('saveBtn');
const saveStatus = document.getElementById('saveStatus');

function renderAdminGradeTable(){
  if(data.students.length === 0){
    adminGradesTable.innerHTML = '<tr><td style="border:none;padding:16px;color:var(--ink-dim);">Hali talaba qo\'shilmagan.</td></tr>';
    return;
  }

  let thead = '<tr><th>Ism</th><th>Guruh</th>';
  data.units.forEach(u => { thead += `<th>${escapeHtml(u)}</th>`; });
  thead += '<th></th></tr>';

  let tbody = '';
  data.students.forEach(s => {
    tbody += `<tr><td class="name-cell">${escapeHtml(s.name)}</td><td class="group-cell">${escapeHtml(s.group)}</td>`;
    data.units.forEach(u => {
      const val = (s.scores && s.scores[u] !== undefined) ? s.scores[u] : '';
      tbody += `<td><input type="number" min="0" max="100" data-student="${s.id}" data-unit="${escapeHtml(u)}" value="${val}"></td>`;
    });
    tbody += `<td><button class="danger" data-del-student="${s.id}">O'chirish</button></td></tr>`;
  });

  adminGradesTable.innerHTML = '<thead>' + thead + '</thead><tbody>' + tbody + '</tbody>';

  adminGradesTable.querySelectorAll('input[type="number"]').forEach(inp => {
    inp.addEventListener('input', () => {
      const sid = inp.dataset.student;
      const unit = inp.dataset.unit;
      const student = data.students.find(x => x.id === sid);
      if(!student) return;
      if(!student.scores) student.scores = {};
      if(inp.value === ''){ delete student.scores[unit]; }
      else { student.scores[unit] = Math.max(0, Math.min(100, Number(inp.value))); }
    });
  });

  adminGradesTable.querySelectorAll('[data-del-student]').forEach(btn => {
    btn.addEventListener('click', async () => {
      const sid = btn.dataset.delStudent;
      const student = data.students.find(x => x.id === sid);
      if(!student) return;
      if(!confirm(`${student.name} o'chirilsinmi?`)) return;
      data.students = data.students.filter(x => x.id !== sid);
      renderAdminGradeTable();
      await saveData();
    });
  });
}

saveBtn.addEventListener('click', async () => {
  saveBtn.disabled = true;
  saveStatus.textContent = 'Saqlanmoqda…';
  const ok = await saveData();
  saveStatus.textContent = ok ? "Saqlandi ✓" : "Xatolik yuz berdi, qayta urinib ko'ring.";
  saveBtn.disabled = false;
  setTimeout(() => { saveStatus.textContent = ''; }, 2500);
});

/* ---------------- init ---------------- */
if(firebaseNotConfigured){
  document.getElementById('setupNotice').style.display = 'block';
}
loadData();
</script>
</body>
</html>
