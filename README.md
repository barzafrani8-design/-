<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>סידור עבודה</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:system-ui,-apple-system,sans-serif;background:#f5f5f3;color:#1a1a1a;direction:rtl;padding:1rem}
.app{max-width:860px;margin:0 auto}
h1{font-size:18px;font-weight:500;text-align:center;margin-bottom:1.25rem;color:#1a1a1a}
.tabs{display:flex;gap:6px;margin-bottom:1rem}
.tab{flex:1;padding:8px;border:0.5px solid #ccc;border-radius:8px;font-size:13px;cursor:pointer;background:#fff;color:#666;text-align:center}
.tab.active{background:#e8f0fe;color:#1a56db;border-color:#a4c2f4;font-weight:500}
.card{background:#fff;border:0.5px solid #e0e0e0;border-radius:12px;padding:1rem;margin-bottom:0.85rem}
.section-title{font-size:12px;font-weight:500;color:#666;margin-bottom:8px;text-transform:uppercase;letter-spacing:0.04em}
.workers-row{display:flex;gap:6px;margin-bottom:8px;flex-wrap:wrap;align-items:center;min-height:24px}
.worker-input{display:flex;gap:6px;align-items:center}
.worker-input input{width:110px;font-size:13px;padding:5px 8px;border:0.5px solid #ccc;border-radius:6px;outline:none}
.worker-input input:focus{border-color:#1a56db}
.tag{border-radius:999px;padding:3px 8px 3px 6px;font-size:13px;display:flex;align-items:center;gap:4px;background:#f0f0ee;border:0.5px solid #ccc;color:#1a1a1a}
.tag button{background:none;border:none;cursor:pointer;color:#888;font-size:12px;padding:0;line-height:1}
button{padding:5px 14px;border:0.5px solid #ccc;border-radius:6px;font-size:13px;cursor:pointer;background:#fff;color:#333;font-family:inherit}
button:hover{background:#f5f5f3}
.opts-row{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.tog{padding:5px 14px;border:0.5px solid #ccc;border-radius:6px;font-size:13px;cursor:pointer;background:#fff;color:#666}
.tog.on{background:#e8f0fe;color:#1a56db;border-color:#a4c2f4}
.divider{border:none;border-top:0.5px solid #e0e0e0;margin:10px 0}
.warn{color:#c0392b;font-size:12px;margin-top:4px}
.hidden{display:none}
.panel{display:none}
.panel.active{display:block}

/* עמדות */
.tbl-wrap{overflow-x:auto}
table{border-collapse:collapse;width:100%}
th,td{border:0.5px solid #e0e0e0;text-align:center;vertical-align:middle}
th{background:#f5f5f3;font-size:11px;font-weight:500;color:#666;padding:5px 4px;white-space:nowrap}
td.row-label{background:#f5f5f3;font-size:12px;font-weight:500;color:#1a1a1a;padding:5px 8px;white-space:nowrap;text-align:right}
td.cell{padding:0;min-width:80px}
select{font-family:inherit;font-size:13px}
.cell-select{width:100%;border:none;background:transparent;font-size:13px;font-weight:500;color:#1a1a1a;padding:7px 4px;text-align:center;cursor:pointer;appearance:none;-webkit-appearance:none}
.cell-select.repeat{background:#fdecea;color:#c0392b}
td.cell-closed{background:#f5f5f3;min-width:80px;padding:7px 4px;font-size:12px;color:#999}

/* סריקות */
.scan-blocks{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.scan-block{border:0.5px solid #e0e0e0;border-radius:8px;overflow:hidden}
.scan-block-header{background:#f5f5f3;text-align:center;padding:6px 4px;font-size:11px;font-weight:500;color:#1a1a1a;border-bottom:0.5px solid #e0e0e0}
.scan-header-row{display:flex;align-items:center;background:#f5f5f3;border-bottom:0.5px solid #e0e0e0}
.scan-hdr-floor{min-width:52px;width:52px;flex-shrink:0;font-size:11px;font-weight:500;color:#666;text-align:center;padding:4px 2px;border-left:0.5px solid #e0e0e0}
.scan-hdr-worker{flex:1;font-size:11px;font-weight:500;color:#666;text-align:center;padding:4px 2px;border-left:0.5px solid #e0e0e0}
.scan-hdr-rm{width:22px;flex-shrink:0}
.scan-row{display:flex;align-items:center;border-top:0.5px solid #e0e0e0}
.sc-floor-cell{min-width:52px;width:52px;flex-shrink:0;background:#f5f5f3;border-left:0.5px solid #e0e0e0;text-align:center;padding:0}
.sc-floor-cell input{width:52px;border:none;background:transparent;font-size:12px;font-weight:500;color:#1a1a1a;text-align:center;padding:6px 3px;outline:none;display:block}
.sc-worker-cell{flex:1;border-left:0.5px solid #e0e0e0}
.sc-select{width:100%;border:none;background:transparent;font-size:13px;font-weight:500;color:#1a1a1a;padding:6px 3px;text-align:center;cursor:pointer;appearance:none;-webkit-appearance:none}
.sc-select.repeat{background:#fdecea;color:#c0392b}
.sc-rm-cell{width:22px;flex-shrink:0;border-left:0.5px solid #e0e0e0;text-align:center}
.sc-rm-btn{border:none;background:transparent;cursor:pointer;color:#999;font-size:13px;padding:4px 3px;width:100%}
.scan-add-row{border-top:0.5px dashed #e0e0e0}
.scan-add-btn{width:100%;border:none;background:transparent;font-size:11px;color:#999;padding:5px;cursor:pointer}
.scan-add-btn:hover{background:#f5f5f3}

/* E28 */
.e28-row{display:flex;align-items:center;gap:10px;padding:8px 10px;background:#f5f5f3;border-radius:8px;margin-top:8px;flex-wrap:wrap}
.e28-row span{font-size:13px;color:#1a1a1a;font-weight:500}
.e28-btn{padding:5px 16px;border:0.5px solid #ccc;border-radius:6px;font-size:13px;cursor:pointer;background:#fff;color:#666}
.e28-btn.sel{border-color:#888;color:#1a1a1a;font-weight:500;box-shadow:0 0 0 1.5px #ccc}

.generate-btn{width:100%;padding:10px;font-size:14px;margin-bottom:0.5rem;border-radius:8px}
.generate-btn.primary{background:#1a56db;color:#fff;border-color:#1a56db}
.generate-btn.primary:hover{background:#1648c0}
.summary{font-size:13px;color:#666;padding:8px 10px;background:#f5f5f3;border-radius:8px;line-height:1.8;margin-top:0.5rem}

@media(max-width:600px){
  .scan-blocks{grid-template-columns:1fr}
  .tabs{flex-direction:column}
}
</style>
</head>
<body>
<div class="app">
  <h1>📋 סידור עבודה</h1>

  <div class="card">
    <div class="section-title">עובדים — עמדות + סריקות (עד 5)</div>
    <div class="workers-row" id="workerTags"></div>
    <div class="worker-input">
      <input type="text" id="wInput" placeholder="שם עובד..." maxlength="12"/>
      <button onclick="addWorker()">+ הוסף</button>
    </div>
    <div class="warn hidden" id="warnTxt"></div>
    <hr class="divider"/>
    <div class="section-title">אחמש — סריקות בלבד</div>
    <div class="workers-row" id="ahmadTags"></div>
    <div class="worker-input">
      <input type="text" id="aInput" placeholder="שם אחמש..." maxlength="12"/>
      <button onclick="addAhmad()">+ הוסף אחמש</button>
    </div>
  </div>

  <div class="card">
    <div class="section-title">הגדרות יומיות</div>
    <div class="opts-row">
      <button class="tog" id="tog-escort" onclick="toggleOpt('escort')">ליווי</button>
    </div>
    <div class="e28-row">
      <span>E-28 נסגר ב:</span>
      <button class="e28-btn sel" id="e28-18" onclick="setE28(18)">18:00</button>
      <button class="e28-btn" id="e28-21" onclick="setE28(21)">21:00</button>
      <button class="e28-btn" id="e28-open" onclick="setE28(0)">פתוח כל היום</button>
    </div>
  </div>

  <div class="tabs">
    <button class="tab active" onclick="switchTab('morning')">☀️ בוקר 07:00–15:00</button>
    <button class="tab" onclick="switchTab('afternoon')">🌆 צהריים 15:00–23:00</button>
  </div>

  <div id="panel-morning" class="panel active">
    <div class="card">
      <div class="section-title">עמדות קבועות — בוקר</div>
      <div class="tbl-wrap" id="st-morning"></div>
    </div>
    <div class="card">
      <div class="section-title">סריקות — בוקר</div>
      <div class="scan-blocks" id="scans-morning"></div>
    </div>
  </div>

  <div id="panel-afternoon" class="panel">
    <div class="card">
      <div class="section-title">עמדות קבועות — צהריים</div>
      <div class="tbl-wrap" id="st-afternoon"></div>
    </div>
    <div class="card">
      <div class="section-title">סריקות — צהריים</div>
      <div class="scan-blocks" id="scans-afternoon"></div>
    </div>
  </div>

  <button class="generate-btn primary" onclick="autoFill()">✨ חלק אוטומטית</button>
  <button class="generate-btn" onclick="clearAll()">↺ נקה שיבוצים</button>
  <div class="summary hidden" id="summary"></div>
</div>

<script>
let workers=[],ahmads=[];
let opts={escort:false};
let e28Close=18;
let curTab='morning';

let scanFloors={
  morning:[['19-20','21-22','23-25','26-28'],['19-20','21-22','23-25','26-28'],['19-20','21-22','23-25','26-28']],
  afternoon:[['19-20','21-22','23-25','26-28'],['19-20','21-22','23-25','26-28'],['19-20','21-22','23-25','26-28']]
};
let scanAssign={morning:[[],[],[]],afternoon:[[],[],[]]};

const MST=['07:00–09:00','09:00–11:00','11:00–13:00','13:00–15:00'];
const AST=['15:00–17:00','17:00–19:00','19:00–21:00','21:00–23:00'];
const MSC=['07:00–09:00','09:00–12:00','12:00–15:00'];
const ASC=['15:00–17:00','17:00–20:00','20:00–23:00'];
const FIXED=['קבלה','תחנות 19-23','עליונות 24-28','E-28'];

function getStations(){const s=[...FIXED];if(opts.escort)s.push('ליווי');return s;}
function allScan(){return[...workers,...ahmads];}
function safeId(s){return s.replace(/[^a-z0-9]/gi,'_');}
function slotStart(slot){return parseInt(slot.split(':')[0]);}
function isE28Closed(row,slot){if(row!=='E-28'||e28Close===0)return false;return slotStart(slot)>=e28Close;}

document.getElementById('wInput').addEventListener('keydown',e=>{if(e.key==='Enter')addWorker();});
document.getElementById('aInput').addEventListener('keydown',e=>{if(e.key==='Enter')addAhmad();});

function addWorker(){
  const inp=document.getElementById('wInput'),n=inp.value.trim(),w=document.getElementById('warnTxt');
  if(!n)return;
  if(workers.length>=5){w.textContent='מקסימום 5';w.classList.remove('hidden');return;}
  if(workers.includes(n)||ahmads.includes(n)){w.textContent='השם קיים';w.classList.remove('hidden');inp.value='';return;}
  w.classList.add('hidden');workers.push(n);inp.value='';renderAll();
}
function addAhmad(){
  const inp=document.getElementById('aInput'),n=inp.value.trim();
  if(!n||workers.includes(n)||ahmads.includes(n))return;
  ahmads.push(n);inp.value='';renderAll();
}
function removeWorker(n){workers=workers.filter(w=>w!==n);renderAll();}
function removeAhmad(n){ahmads=ahmads.filter(w=>w!==n);renderAll();}

function renderTags(){
  document.getElementById('workerTags').innerHTML=workers.map(w=>`<span class="tag">${w}<button onclick="removeWorker('${w}')">✕</button></span>`).join('');
  document.getElementById('ahmadTags').innerHTML=ahmads.map(a=>`<span class="tag">${a}<button onclick="removeAhmad('${a}')">✕</button></span>`).join('');
}
function toggleOpt(k){opts[k]=!opts[k];document.getElementById('tog-'+k).classList.toggle('on',opts[k]);renderAll();}
function switchTab(t){
  curTab=t;
  document.querySelectorAll('.tab').forEach((el,i)=>el.classList.toggle('active',(i===0&&t==='morning')||(i===1&&t==='afternoon')));
  document.getElementById('panel-morning').classList.toggle('active',t==='morning');
  document.getElementById('panel-afternoon').classList.toggle('active',t==='afternoon');
}
function setE28(val){
  e28Close=val;
  ['e28-18','e28-21','e28-open'].forEach(id=>document.getElementById(id).classList.remove('sel'));
  document.getElementById({18:'e28-18',21:'e28-21',0:'e28-open'}[val]).classList.add('sel');
  renderStTable('morning');renderStTable('afternoon');
}

function renderStTable(shift){
  const el=document.getElementById('st-'+shift);if(!el)return;
  const slots=shift==='morning'?MST:AST;
  const pfx=shift==='morning'?'stm':'sta';
  const rows=getStations();
  const wo=['—',...workers];
  let h=`<table><thead><tr><th style="min-width:90px">עמדה</th>${slots.map(s=>`<th>${s}</th>`).join('')}</tr></thead><tbody>`;
  for(const r of rows){
    h+=`<tr><td class="row-label">${r}</td>`;
    for(const s of slots){
      if(isE28Closed(r,s)){
        h+=`<td class="cell-closed">סגור</td>`;
      } else {
        const id=pfx+'_'+safeId(r)+'_'+safeId(s);
        h+=`<td class="cell"><select class="cell-select" id="${id}" onchange="validateSt('${pfx}')">${wo.map(o=>`<option>${o}</option>`).join('')}</select></td>`;
      }
    }
    h+='</tr>';
  }
  h+='</tbody></table>';el.innerHTML=h;
}

function renderScans(shift){
  const slots=shift==='morning'?MSC:ASC;
  const c=document.getElementById('scans-'+shift);if(!c)return;
  const wo=['—',...allScan()];
  let html='';
  for(let i=0;i<3;i++){
    const floors=scanFloors[shift][i];
    const assigns=scanAssign[shift][i]||[];
    html+=`<div class="scan-block">
      <div class="scan-block-header">${slots[i]}</div>
      <div class="scan-header-row">
        <div class="scan-hdr-floor">קומה</div>
        <div class="scan-hdr-worker">עובד</div>
        <div class="scan-hdr-rm"></div>
      </div>`;
    for(let f=0;f<floors.length;f++){
      const val=assigns[f]||'—';
      html+=`<div class="scan-row">
        <div class="sc-floor-cell"><input type="text" value="${floors[f]}" onchange="updateFloor('${shift}',${i},${f},this.value)"/></div>
        <div class="sc-worker-cell"><select class="sc-select" onchange="setAssign('${shift}',${i},${f},this.value)">${wo.map(o=>`<option${o===val?' selected':''}>${o}</option>`).join('')}</select></div>
        <div class="sc-rm-cell"><button class="sc-rm-btn" onclick="removeFloor('${shift}',${i},${f})">×</button></div>
      </div>`;
    }
    html+=`<div class="scan-add-row"><button class="scan-add-btn" onclick="addFloor('${shift}',${i})">+ קומה</button></div></div>`;
  }
  c.innerHTML=html;
}

function updateFloor(shift,si,fi,val){scanFloors[shift][si][fi]=val;}
function setAssign(shift,si,fi,val){
  if(!scanAssign[shift][si])scanAssign[shift][si]=[];
  scanAssign[shift][si][fi]=val==='—'?'':val;
  validateScan(shift,si);
}
function addFloor(shift,si){
  scanFloors[shift][si].push('');
  if(!scanAssign[shift][si])scanAssign[shift][si]=[];
  scanAssign[shift][si].push('');
  renderScans(shift);
}
function removeFloor(shift,si,fi){
  scanFloors[shift][si].splice(fi,1);
  if(scanAssign[shift][si])scanAssign[shift][si].splice(fi,1);
  renderScans(shift);
}

function renderAll(){
  renderTags();
  renderStTable('morning');renderStTable('afternoon');
  renderScans('morning');renderScans('afternoon');
}

function smartSt(shift){
  const slots=shift==='morning'?MST:AST;
  const pfx=shift==='morning'?'stm':'sta';
  const rows=getStations();
  const done={};rows.forEach(r=>done[r]=new Set());
  const cnt={};workers.forEach(w=>cnt[w]=0);
  for(const slot of slots){
    const used=new Set();
    for(const row of [...rows].sort(()=>Math.random()-0.5)){
      if(isE28Closed(row,slot))continue;
      let c=workers.filter(w=>!done[row].has(w)&&!used.has(w));
      if(!c.length)c=workers.filter(w=>!used.has(w));
      if(!c.length)continue;
      c.sort((a,b)=>cnt[a]-cnt[b]);
      const ch=c[0];
      const el=document.getElementById(pfx+'_'+safeId(row)+'_'+safeId(slot));
      if(el)el.value=ch;
      done[row].add(ch);used.add(ch);cnt[ch]++;
    }
  }
}
function smartScan(shift){
  const all=allScan();if(!all.length)return;
  const done={};const cnt={};all.forEach(w=>cnt[w]=0);
  for(let i=0;i<3;i++){
    const floors=scanFloors[shift][i];
    if(!scanAssign[shift][i])scanAssign[shift][i]=[];
    const used=new Set();
    for(let f=0;f<floors.length;f++){
      const fl=floors[f]||f;
      if(!done[fl])done[fl]=new Set();
      let c=all.filter(w=>!done[fl].has(w)&&!used.has(w));
      if(!c.length)c=all.filter(w=>!used.has(w));
      if(!c.length)continue;
      c.sort((a,b)=>cnt[a]-cnt[b]);
      const ch=c[0];
      scanAssign[shift][i][f]=ch;
      done[fl].add(ch);used.add(ch);cnt[ch]++;
    }
  }
  renderScans(shift);
}

function autoFill(){
  if(!workers.length&&!ahmads.length){alert('יש להוסיף עובדים');return;}
  const sh=curTab==='morning'?'morning':'afternoon';
  if(workers.length)smartSt(sh);
  smartScan(sh);
  validateSt(sh==='morning'?'stm':'sta');
  [0,1,2].forEach(i=>validateScan(sh,i));
  showSummary();
}
function validateSt(pfx){
  document.querySelectorAll(`[id^="${pfx}_"]`).forEach(s=>s.classList.remove('repeat'));
  const byRow={};
  document.querySelectorAll(`[id^="${pfx}_"]`).forEach(s=>{
    const k=s.id.replace(pfx+'_','').split('_').slice(0,-2).join('_');
    if(!byRow[k])byRow[k]=[];byRow[k].push(s);
  });
  for(const r of Object.values(byRow)){
    const seen={};
    for(const s of r){const v=s.value;if(v==='—')continue;if(seen[v]){s.classList.add('repeat');seen[v].classList.add('repeat');}else seen[v]=s;}
  }
}
function validateScan(shift,si){
  const blocks=document.querySelectorAll(`#scans-${shift} .scan-block`);
  if(!blocks[si])return;
  const sels=blocks[si].querySelectorAll('.sc-select');
  const seen={};
  sels.forEach(s=>{
    s.classList.remove('repeat');
    const v=s.value;if(v==='—')return;
    if(seen[v]){s.classList.add('repeat');seen[v].classList.add('repeat');}
    else seen[v]=s;
  });
}
function clearAll(){
  document.querySelectorAll('.cell-select').forEach(s=>s.value='—');
  scanAssign={morning:[[],[],[]],afternoon:[[],[],[]]};
  renderScans('morning');renderScans('afternoon');
  document.getElementById('summary').classList.add('hidden');
}
function showSummary(){
  const cnt={};[...workers,...ahmads].forEach(w=>cnt[w]=0);
  document.querySelectorAll('.cell-select').forEach(s=>{if(s.value!=='—'&&cnt[s.value]!==undefined)cnt[s.value]++;});
  ['morning','afternoon'].forEach(sh=>[0,1,2].forEach(i=>(scanAssign[sh][i]||[]).forEach(w=>{if(w&&cnt[w]!==undefined)cnt[w]++;})));
  const sumEl=document.getElementById('summary');sumEl.classList.remove('hidden');
  sumEl.innerHTML='<strong>סיכום:</strong> '+[...workers,...ahmads].map(w=>`${w}: ${cnt[w]} תורנויות`).join(' · ')+'<br><small style="color:#c0392b">■ אדום = חזרה על אותה עמדה</small>';
}
renderAll();
</script>
</body>
</html>
