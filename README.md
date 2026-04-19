<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>開栓作業 お客様アンケート</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
:root {
  --gas-green: #1D9E75;
  --gas-green-light: #E1F5EE;
  --gas-green-dark: #085041;
  --gas-amber: #BA7517;
  --gas-amber-light: #FAEEDA;
  --gas-amber-dark: #633806;
  --gas-purple: #534AB7;
  --text: #1a1a1a;
  --text-sub: #666;
  --text-hint: #999;
  --bg: #f7f7f5;
  --surface: #fff;
  --border: rgba(0,0,0,0.12);
  --border-strong: rgba(0,0,0,0.22);
  --radius: 10px;
  --radius-lg: 16px;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: 'Noto Sans JP', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  padding-bottom: 3rem;
}
.header {
  background: var(--gas-green);
  color: #fff;
  padding: 1rem 1.25rem 0.875rem;
  display: flex;
  align-items: center;
  gap: 10px;
}
.header-icon {
  width: 32px; height: 32px;
  background: rgba(255,255,255,0.2);
  border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
}
.header h1 { font-size: 15px; font-weight: 700; }
.header p { font-size: 11px; opacity: 0.85; margin-top: 1px; }
.staff-bar {
  background: var(--gas-green-dark);
  padding: 0.5rem 1.25rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 12px;
  color: rgba(255,255,255,0.85);
}
.staff-id-badge {
  background: rgba(255,255,255,0.15);
  border-radius: 4px;
  padding: 2px 8px;
  font-weight: 500;
  color: #fff;
}
.container { max-width: 480px; margin: 0 auto; padding: 1.25rem 1rem; }
.prog-wrap { margin-bottom: 1.5rem; }
.prog-label { display: flex; justify-content: space-between; font-size: 12px; color: var(--text-sub); margin-bottom: 6px; }
.prog-track { height: 5px; background: var(--border); border-radius: 3px; }
.prog-fill { height: 5px; background: var(--gas-green); border-radius: 3px; transition: width 0.4s ease; }
.step { display: none; }
.step.active { display: block; }
.card {
  background: var(--surface);
  border-radius: var(--radius-lg);
  border: 0.5px solid var(--border);
  padding: 1.25rem;
  margin-bottom: 1rem;
}
.q-badge {
  display: inline-block;
  background: var(--gas-green-light);
  color: var(--gas-green-dark);
  font-size: 11px;
  font-weight: 700;
  padding: 2px 8px;
  border-radius: 4px;
  margin-bottom: 8px;
}
.q-text {
  font-size: 15px;
  font-weight: 500;
  line-height: 1.55;
  margin-bottom: 1.25rem;
  color: var(--text);
}
.star-row { display: flex; gap: 8px; margin-bottom: 0.5rem; }
.star {
  font-size: 38px;
  cursor: pointer;
  color: #ddd;
  transition: color 0.1s, transform 0.1s;
  user-select: none;
  line-height: 1;
}
.star.on { color: #EF9F27; }
.star:active { transform: scale(0.9); }
.star-hint { display: flex; justify-content: space-between; font-size: 11px; color: var(--text-hint); margin-bottom: 1.25rem; }
.opt {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
  text-align: left;
  padding: 13px 14px;
  margin-bottom: 8px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  font-size: 14px;
  color: var(--text);
  cursor: pointer;
  transition: border-color 0.15s, background 0.15s;
  font-family: inherit;
}
.opt:last-of-type { margin-bottom: 0; }
.opt-radio {
  width: 18px; height: 18px;
  border-radius: 50%;
  border: 2px solid var(--border-strong);
  flex-shrink: 0;
  transition: border-color 0.15s, background 0.15s;
}
.opt.sel { border-color: var(--gas-green); background: var(--gas-green-light); }
.opt.sel .opt-radio { border-color: var(--gas-green); background: var(--gas-green); }
.opt:hover:not(.sel) { background: #f9f9f9; border-color: var(--border-strong); }
.notice-box {
  background: #EAF3DE;
  border: 1px solid #97C459;
  border-radius: var(--radius);
  padding: 12px 14px;
  font-size: 13px;
  color: #27500A;
  margin-top: 12px;
  display: none;
  line-height: 1.6;
}
.notice-box.show { display: block; }
textarea {
  width: 100%;
  min-height: 80px;
  padding: 10px 12px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius);
  font-size: 14px;
  color: var(--text);
  font-family: inherit;
  resize: vertical;
  margin-top: 0.75rem;
}
textarea:focus { outline: none; border-color: var(--gas-green); }
.next-btn {
  width: 100%;
  padding: 15px;
  background: var(--gas-green);
  color: #fff;
  border: none;
  border-radius: var(--radius);
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  font-family: inherit;
  transition: opacity 0.15s;
  margin-top: 1rem;
  letter-spacing: 0.02em;
}
.next-btn:disabled { opacity: 0.35; cursor: not-allowed; }
.next-btn:not(:disabled):active { opacity: 0.85; }
.slot-wrap {
  background: var(--surface);
  border-radius: var(--radius-lg);
  border: 0.5px solid var(--border);
  padding: 1.5rem 1.25rem;
  text-align: center;
}
.slot-title { font-size: 17px; font-weight: 700; margin-bottom: 4px; }
.slot-sub { font-size: 13px; color: var(--text-sub); margin-bottom: 4px; }
.slot-prob { font-size: 12px; color: var(--text-hint); }
.reels {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin: 1.25rem 0;
}
.reel {
  width: 80px; height: 90px;
  background: var(--bg);
  border: 1px solid var(--border-strong);
  border-radius: var(--radius);
  display: flex; align-items: center; justify-content: center;
  font-size: 46px;
  overflow: hidden;
  position: relative;
}
.reel.spinning { animation: shake 0.12s infinite; }
@keyframes shake {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-2px); }
}
.reel.stopped { animation: pop 0.25s ease; }
@keyframes pop {
  0% { transform: scale(1.12); }
  100% { transform: scale(1); }
}
.spin-btn {
  width: 100%;
  padding: 15px;
  background: var(--gas-purple);
  color: #fff;
  border: none;
  border-radius: var(--radius);
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  font-family: inherit;
  letter-spacing: 0.03em;
  transition: opacity 0.15s;
}
.spin-btn:disabled { opacity: 0.35; cursor: not-allowed; }
.result-panel {
  border-radius: var(--radius-lg);
  padding: 2rem 1.25rem;
  text-align: center;
}
.result-win { background: var(--gas-amber-light); border: 1px solid #EF9F27; }
.result-lose { background: var(--surface); border: 0.5px solid var(--border); }
.result-icon { font-size: 52px; margin-bottom: 12px; }
.result-h { font-size: 19px; font-weight: 700; margin-bottom: 8px; }
.result-win .result-h { color: var(--gas-amber-dark); }
.result-lose .result-h { color: var(--text); }
.result-p { font-size: 14px; line-height: 1.7; }
.result-win .result-p { color: var(--gas-amber); }
.result-lose .result-p { color: var(--text-sub); }
.win-ticket {
  background: #fff;
  border: 1.5px dashed #EF9F27;
  border-radius: var(--radius);
  padding: 14px 16px;
  margin-top: 16px;
  display: inline-block;
  min-width: 220px;
}
.win-ticket-label { font-size: 11px; color: var(--gas-amber); font-weight: 700; letter-spacing: 0.05em; margin-bottom: 4px; }
.win-ticket-code { font-size: 20px; font-weight: 700; color: var(--gas-amber-dark); letter-spacing: 0.1em; }
.win-ticket-time { font-size: 11px; color: var(--text-hint); margin-top: 4px; }
.csv-section { margin-top: 1.5rem; }
.csv-btn {
  width: 100%;
  padding: 13px;
  background: var(--surface);
  color: var(--gas-green-dark);
  border: 1.5px solid var(--gas-green);
  border-radius: var(--radius);
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
  font-family: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  margin-bottom: 10px;
}
.csv-btn:active { opacity: 0.8; }
.qr-section {
  background: var(--surface);
  border-radius: var(--radius-lg);
  border: 0.5px solid var(--border);
  padding: 1.25rem;
  text-align: center;
  margin-bottom: 1rem;
}
.qr-title { font-size: 14px; font-weight: 500; margin-bottom: 4px; }
.qr-sub { font-size: 12px; color: var(--text-sub); margin-bottom: 12px; }
#qrcode { display: flex; justify-content: center; margin-bottom: 10px; }
.qr-url { font-size: 11px; color: var(--text-hint); word-break: break-all; }
.modal-overlay {
  display: none;
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.5);
  z-index: 100;
  align-items: center;
  justify-content: center;
}
.modal-overlay.show { display: flex; }
.modal {
  background: var(--surface);
  border-radius: var(--radius-lg);
  padding: 1.5rem;
  width: 90%;
  max-width: 360px;
}
.modal h3 { font-size: 16px; font-weight: 700; margin-bottom: 8px; }
.modal p { font-size: 14px; color: var(--text-sub); margin-bottom: 1rem; line-height: 1.6; }
.modal input {
  width: 100%;
  padding: 12px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius);
  font-size: 15px;
  font-family: inherit;
  margin-bottom: 10px;
}
.modal input:focus { outline: none; border-color: var(--gas-green); }
.modal-btn {
  width: 100%;
  padding: 13px;
  background: var(--gas-green);
  color: #fff;
  border: none;
  border-radius: var(--radius);
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  font-family: inherit;
}
.tag { font-size: 11px; }
</style>
</head>
<body>

<div class="header">
  <div class="header-icon">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2a8 8 0 0 1 8 8c0 5-8 12-8 12S4 15 4 10a8 8 0 0 1 8-8z"/><circle cx="12" cy="10" r="3"/></svg>
  </div>
  <div>
    <h1>開栓作業 お客様アンケート</h1>
    <p>ご回答後にスロット抽選へご参加いただけます</p>
  </div>
</div>
<div class="staff-bar">
  <span>担当者情報</span>
  <span class="staff-id-badge" id="staff-display">—</span>
</div>

<div class="container">

  <!-- QRコード生成セクション（担当者向け） -->
  <div id="qr-section" class="qr-section" style="display:none;">
    <div class="qr-title">お客様用QRコード</div>
    <div class="qr-sub">このコードをお客様のスマホで読み取っていただいてください</div>
    <div id="qrcode"></div>
    <div class="qr-url" id="qr-url-text"></div>
  </div>

  <!-- Step: アンケート -->
  <div class="prog-wrap" id="prog-wrap">
    <div class="prog-label">
      <span id="prog-label-left">アンケート</span>
      <span id="prog-label-right">1 / 5</span>
    </div>
    <div class="prog-track"><div class="prog-fill" id="prog" style="width:0%"></div></div>
  </div>

  <div class="step active" id="s1">
    <div class="card">
      <div class="q-badge">Q1 担当者の対応</div>
      <div class="q-text">本日の担当者の対応はいかがでしたか？</div>
      <div class="star-row" id="sr1">
        <span class="star" data-v="1">★</span>
        <span class="star" data-v="2">★</span>
        <span class="star" data-v="3">★</span>
        <span class="star" data-v="4">★</span>
        <span class="star" data-v="5">★</span>
      </div>
      <div class="star-hint"><span>不満</span><span>大変満足</span></div>
    </div>
    <button class="next-btn" id="n1" onclick="nxt(1)" disabled>次へ</button>
  </div>

  <div class="step" id="s2">
    <div class="card">
      <div class="q-badge">Q2 総合満足度</div>
      <div class="q-text">今回の開栓作業の全体的なご満足度を教えてください。</div>
      <div class="star-row" id="sr2">
        <span class="star" data-v="1">★</span>
        <span class="star" data-v="2">★</span>
        <span class="star" data-v="3">★</span>
        <span class="star" data-v="4">★</span>
        <span class="star" data-v="5">★</span>
      </div>
      <div class="star-hint"><span>不満</span><span>大変満足</span></div>
      <div style="font-size:13px;color:var(--text-sub);margin-bottom:4px;">ご意見・ご感想（任意）</div>
      <textarea id="comment" placeholder="ご自由にお書きください"></textarea>
    </div>
    <button class="next-btn" id="n2" onclick="nxt(2)" disabled>次へ</button>
  </div>

  <div class="step" id="s3">
    <div class="card">
      <div class="q-badge">Q3 都市ガス警報器</div>
      <div class="q-text">現在、ガス警報器はご自宅に設置されていますか？</div>
      <button class="opt" onclick="sel(3,'installed',this)"><span class="opt-radio"></span>設置している</button>
      <button class="opt" onclick="sel(3,'not_installed',this)"><span class="opt-radio"></span>設置していない</button>
      <button class="opt" onclick="sel(3,'unknown',this)"><span class="opt-radio"></span>わからない</button>
    </div>
    <button class="next-btn" id="n3" onclick="nxt(3)" disabled>次へ</button>
  </div>

  <div class="step" id="s4">
    <div class="card">
      <div class="q-badge">Q4 警報器のご関心</div>
      <div class="q-text">ガス漏れ・不完全燃焼を早期検知する警報器に、ご興味はありますか？</div>
      <button class="opt" onclick="sel(4,'yes',this)"><span class="opt-radio"></span>ぜひ詳しく聞きたい</button>
      <button class="opt" onclick="sel(4,'maybe',this)"><span class="opt-radio"></span>機会があれば検討したい</button>
      <button class="opt" onclick="sel(4,'no',this)"><span class="opt-radio"></span>今は必要ない</button>
      <div class="notice-box" id="notice-q4">
        <strong>📋 担当者より折り返しご案内いたします</strong><br>
        警報器の詳細・設置費用・補助金情報などをご説明します。後日ご連絡させていただきますので、今後ともよろしくお願いいたします。
      </div>
    </div>
    <button class="next-btn" id="n4" onclick="nxt(4)" disabled>次へ</button>
  </div>

  <div class="step" id="s5">
    <div class="card">
      <div class="q-badge">Q5 宅配水サービス</div>
      <div class="q-text">自宅にウォーターサーバーを置く「宅配水サービス」に、ご興味はありますか？</div>
      <button class="opt" onclick="sel(5,'yes',this)"><span class="opt-radio"></span>ぜひ詳しく聞きたい</button>
      <button class="opt" onclick="sel(5,'maybe',this)"><span class="opt-radio"></span>機会があれば検討したい</button>
      <button class="opt" onclick="sel(5,'no',this)"><span class="opt-radio"></span>今は必要ない</button>
      <div class="notice-box" id="notice-q5">
        <strong>💧 担当者より折り返しご案内いたします</strong><br>
        宅配水サービスの料金プラン・無料お試しなど詳しくご説明します。後日ご連絡させていただきます。
      </div>
    </div>
    <button class="next-btn" id="n5" onclick="nxt(5)" disabled>アンケート完了 → 抽選へ！</button>
  </div>

  <!-- スロット抽選 -->
  <div class="step" id="s-slot">
    <div class="slot-wrap">
      <div class="slot-title">🎰 スロット抽選</div>
      <div class="slot-sub">ボタンを押してスロットを回してください！</div>
      <div class="slot-prob">当選確率 1%（100回に1回）</div>
      <div class="reels">
        <div class="reel" id="r0">🎰</div>
        <div class="reel" id="r1">🎰</div>
        <div class="reel" id="r2">🎰</div>
      </div>
      <button class="spin-btn" id="spin-btn" onclick="spinSlot()">スロットを回す！</button>
    </div>
  </div>

  <!-- 当選 -->
  <div class="step" id="s-win">
    <div class="result-panel result-win">
      <div class="result-icon">🎁</div>
      <div class="result-h">おめでとうございます！</div>
      <div class="result-p">粗品が当たりました！<br>この画面を担当者にお見せください。</div>
      <div class="win-ticket">
        <div class="win-ticket-label">当選証明番号</div>
        <div class="win-ticket-code" id="win-code">—</div>
        <div class="win-ticket-time" id="win-time">—</div>
      </div>
    </div>
    <div style="margin-top:1rem;font-size:13px;color:var(--gas-green-dark);text-align:center;" id="save-status-win"></div>
  </div>

  <!-- はずれ -->
  <div class="step" id="s-lose">
    <div class="result-panel result-lose">
      <div class="result-icon">😊</div>
      <div class="result-h">残念、はずれでした</div>
      <div class="result-p">アンケートへのご協力、<br>誠にありがとうございました！<br>今後ともよろしくお願いいたします。</div>
    </div>
    <div style="margin-top:1rem;font-size:13px;color:var(--gas-green-dark);text-align:center;" id="save-status-lose"></div>
  </div>

</div>

<!-- 担当者IDモーダル -->
<div class="modal-overlay show" id="modal">
  <div class="modal">
    <h3>担当者IDを入力</h3>
    <p>作業開始前に担当者IDを入力してください。入力後にお客様用QRコードが表示されます。</p>
    <input type="text" id="staff-input" placeholder="例：A001" maxlength="10">
    <div style="font-size:12px;color:var(--text-hint);margin-bottom:12px;">作業日時は自動で記録されます（<span id="modal-time"></span>）</div>
    <button class="modal-btn" onclick="setStaff()">設定してQRコードを表示</button>
  </div>
</div>

<script>
const TOTAL = 5;
const SYMS = ['🍀','⭐','🔔','💎','🌸'];
const WIN_SYM = '💎';
const ans = {};
let staffId = '';
let workDatetime = '';
let spinning = false;
let slotResult = null;

function fmtDate(d) {
  const pad = n => String(n).padStart(2,'0');
  return d.getFullYear() + '/' + pad(d.getMonth()+1) + '/' + pad(d.getDate()) + ' ' + pad(d.getHours()) + ':' + pad(d.getMinutes());
}

window.addEventListener('DOMContentLoaded', () => {
  const now = new Date();
  workDatetime = fmtDate(now);
  document.getElementById('modal-time').textContent = workDatetime;

  const params = new URLSearchParams(location.search);
  if (params.get('staff')) {
    staffId = params.get('staff');
    document.getElementById('staff-input').value = staffId;
    applyStaff();
  }

  [1,2].forEach(q => {
    document.getElementById('sr'+q).querySelectorAll('.star').forEach(s => {
      s.addEventListener('click', () => {
        const v = parseInt(s.dataset.v);
        ans['q'+q] = v;
        document.getElementById('sr'+q).querySelectorAll('.star').forEach(x => {
          x.classList.toggle('on', parseInt(x.dataset.v) <= v);
        });
        document.getElementById('n'+q).disabled = false;
      });
    });
  });

  setProgress(1);
});

function setStaff() {
  const val = document.getElementById('staff-input').value.trim();
  if (!val) { alert('担当者IDを入力してください'); return; }
  staffId = val;
  applyStaff();
}

function applyStaff() {
  document.getElementById('modal').classList.remove('show');
  document.getElementById('staff-display').textContent = staffId + '　' + workDatetime;

  const url = location.origin + location.pathname + '?staff=' + encodeURIComponent(staffId);
  document.getElementById('qr-section').style.display = 'block';
  document.getElementById('qr-url-text').textContent = url;

  const qrEl = document.getElementById('qrcode');
  qrEl.innerHTML = '';
  new QRCode(qrEl, {
    text: url,
    width: 160,
    height: 160,
    colorDark: '#1a1a1a',
    colorLight: '#ffffff',
    correctLevel: QRCode.CorrectLevel.M
  });
}

function setProgress(step) {
  const pct = Math.round(((step-1)/TOTAL)*100);
  document.getElementById('prog').style.width = pct + '%';
  document.getElementById('prog-label-right').textContent = step + ' / ' + TOTAL;
}

function nxt(step) {
  document.getElementById('s'+step).classList.remove('active');
  if (step < TOTAL) {
    document.getElementById('s'+(step+1)).classList.add('active');
    setProgress(step+1);
  } else {
    document.getElementById('prog').style.width = '100%';
    document.getElementById('prog-label-left').textContent = '完了！抽選へ';
    document.getElementById('prog-label-right').textContent = '';
    document.getElementById('s-slot').classList.add('active');
  }
}

function sel(step, val, el) {
  ans['q'+step] = val;
  el.parentElement.querySelectorAll('.opt').forEach(b => b.classList.remove('sel'));
  el.classList.add('sel');
  document.getElementById('n'+step).disabled = false;

  if (step === 4) {
    document.getElementById('notice-q4').classList.toggle('show', val === 'yes');
  }
  if (step === 5) {
    document.getElementById('notice-q5').classList.toggle('show', val === 'yes');
  }
}

function spinSlot() {
  if (spinning) return;
  spinning = true;
  document.getElementById('spin-btn').disabled = true;

  const won = Math.random() < 0.01;
  slotResult = won ? '当選' : 'はずれ';

  const finalSyms = won
    ? [WIN_SYM, WIN_SYM, WIN_SYM]
    : (() => {
        let s;
        do { s = [0,1,2].map(() => SYMS[Math.floor(Math.random()*SYMS.length)]); }
        while (s[0]===s[1] && s[1]===s[2]);
        return s;
      })();

  const durations = [900, 1350, 1800];
  [0,1,2].forEach(i => {
    const el = document.getElementById('r'+i);
    el.classList.add('spinning');
    const iv = setInterval(() => {
      el.textContent = SYMS[Math.floor(Math.random()*SYMS.length)];
    }, 70);
    setTimeout(() => {
      clearInterval(iv);
      el.classList.remove('spinning');
      el.textContent = finalSyms[i];
      el.classList.add('stopped');
      setTimeout(() => el.classList.remove('stopped'), 300);
      if (i === 2) setTimeout(() => showResult(won), 500);
    }, durations[i]);
  });
}

function showResult(won) {
  document.getElementById('s-slot').classList.remove('active');
  if (won) {
    const code = 'WIN-' + staffId + '-' + Date.now().toString(36).toUpperCase().slice(-6);
    document.getElementById('win-code').textContent = code;
    document.getElementById('win-time').textContent = workDatetime;
    ans['winCode'] = code;
    slotResult = '当選';
    document.getElementById('s-win').classList.add('active');
    saveToSheet('save-status-win');
  } else {
    ans['winCode'] = 'はずれ';
    slotResult = 'はずれ';
    document.getElementById('s-lose').classList.add('active');
    saveToSheet('save-status-lose');
  }
}

const GAS_URL = 'https://script.google.com/macros/s/AKfycbyYJquXZj3SF8DJHkfH60vd0jKlllIOLjLAqJPapGJ2Skl2otF_u1-n1KMlterZhwnZ/exec';

const valMap = {
  installed: '設置している', not_installed: '設置していない', unknown: 'わからない',
  yes: '詳しく聞きたい', maybe: '検討したい', no: '必要ない'
};

function saveToSheet(statusId) {
  const payload = {
    staffId: staffId,
    datetime: workDatetime,
    q1: ans.q1 || '',
    q2: ans.q2 || '',
    comment: (document.getElementById('comment').value || ''),
    q3: valMap[ans.q3] || '',
    q4: valMap[ans.q4] || '',
    q5: valMap[ans.q5] || '',
    result: slotResult || '',
    winCode: ans.winCode || ''
  };

  const el = document.getElementById(statusId);
  if (el) el.textContent = '保存中...';

  fetch(GAS_URL, {
    method: 'POST',
    mode: 'no-cors',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  })
  .then(() => {
    if (el) el.textContent = '✓ 回答を保存しました';
  })
  .catch(() => {
    if (el) { el.textContent = '保存に失敗しました（通信エラー）'; el.style.color = '#E24B4A'; }
  });
}
</script>
</body>
</html>
